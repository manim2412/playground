# Dropdown 구현
LanguageInfo.json
```json
[
    { 
        "id": 1, 
        "language": "python", 
        "imgSrc": "/Python.png", 
        "imgAlt": "Python Logo", 
        "version": "3.10.0", 
        "alias": "Python",
        "code": "print('Python');\nfor i in range(2):\n\tprint(i);"
    },
    { 
        "id": 2, 
        "language": "java", 
        "imgSrc": "/Java.png", 
        "imgAlt": "Java Logo", 
        "version": "15.0.2",
        "alias": "Java",
        "code": "public class Main {\n\tpublic static void main(String[] args) {\n\t\tSystem.out.println(\"Java\");\n\t\tfor (int i=0; i<4; i++) {\n\t\t\tSystem.out.println(i);\n\t\t}\n\t}\n}"
    },
    { 
        "id": 3, 
        "language": "javascript", 
        "imgSrc": "/Js.png",
        "imgAlt": "Js Logo", 
        "version": "1.32.3",
        "alias": "Js",
        "code": "console.log('Js');\nfor (let i=0; i<6; i++) {\n\tconsole.log(i);\n}"
    }
]
```

LanguageDropdown.js
```js
import { useEffect, useRef, useState } from 'react';
import { IoMdArrowDropdown } from "react-icons/io";
import useOutSideClick from '@/app/hooks/useOutSideClick';
import Image from 'next/image';

export default function LanguageDropdown({ 
    data, 
    selectedLanguageData,
    setSelectedLanguageData,
    onSelect, // 외부 함수
}) {
    const [isOpen, setIsOpen] = useState(false); 

    const handleChange = (item) => {
        setSelectedLanguageData(item);
        onSelect && onSelect(item);
        setIsOpen(!isOpen); 
    }

    const toggleDropdown = () => {
        setIsOpen(!isOpen)
    }; 
    
    useEffect(() => {
        if (selectedLanguageData && data) {
            const newSelectedLanguageData = data.find((item) => item.id === selectedLanguageData.id);
            newSelectedLanguageData && setSelectedLanguageData(newSelectedLanguageData);
        } 
    }, [selectedLanguageData, data])

    const dropdownRef = useRef(null); 
    useOutSideClick({
        ref: dropdownRef,
        handler: () => setIsOpen(false)
    });

    return (
        <>
            <div className="w-[150px] bg-white shadow-md text-lg border-2 border-solid" ref={dropdownRef}>
                <button className="h-[40px] w-[150px]" onClick={toggleDropdown}>
                    <div className="flex space-x-2 p-2 relative">
                        <span>
                            <Image src={selectedLanguageData.imgSrc} alt={selectedLanguageData.imgAlt} width={25} height={25}/>
                        </span>
                        <span>
                            {selectedLanguageData.alias}
                        </span>
                        <span className={`absolute top-[13px] right-[15px] transition-transform duration-300 ${isOpen ? 'rotate-180' : ''}`}>
                            <IoMdArrowDropdown/>
                        </span>
                    </div>
                </button>
                {isOpen &&
                    <div className="absolute z-50 bg-white shadow-md w-[150px]">
                        {data.map((language) => (
                            <div key={language.id} 
                                className={`hover:cursor-pointer flex ${language.id === selectedLanguageData.id ? "bg-slate-100" : ""}`}
                                onClick={() => {
                                    handleChange(language);
                                }}
                            >
                                <div className="flex space-x-2 p-2">
                                    <span>
                                        <Image src={language.imgSrc} alt={language.imgAlt} height={25} width={25}/>
                                    </span>
                                    <span>
                                        {language.alias}
                                    </span>
                                </div>
                            </div>
                        ))}
                    </div>
                }
            </div>
        </>
    )
}
```

useOutSideClick.js
```js
import { useEffect } from "react"

export default function useOutSideClick({ ref, handler }) {
    useEffect(() => {
        const handleClickOutside = (e) => {
            if (ref.current && !ref.current.contains(e.target)) {
                handler();
            }
        };
        document.addEventListener("mousedown", handleClickOutside); 

        return () => {
            document.removeEventListener("mousedown", handleClickOutside); 
        };
    }, [ref, handler])
}
```

# Online Ide 구현 (piston api 이용)
@/app/onlineide/page.js
```js
"use client";
import Navbar from "../components/Navbar"
import { useState, useRef } from "react";
import Output from "../components/code/Output";
import data from "@/app/data/LanguageInfo.json"
import LanguageDropdown from "../components/dropdown/LanguageDropdown";
import CodeRunButton from "../components/button/CodeRunButton";
import CodeEditor from "../components/code/CodeEditor";
import { executeCode } from "../api/Api";

export default function OnelineIde() {
    const [selectedLanguageData, setSelectedLanguageData] = useState(data[0]); 
    const [code, setCode] = useState(data[0].code);
    const [output, setOutput] = useState(null); 
    const [isLoading, setIsLoading] = useState(false); 
    const [isError, setIsError] = useState(false); 
    const editorRef = useRef();

    const handleSelect = (item) => {
        setCode(item.code); 
        console.log(`selected item info ${item.language}`);
    }

    const runCode = async () => {
        const sourceCode = editorRef.current.getValue();
        console.log(sourceCode); 
        if (!sourceCode) return;
        try {
            setIsLoading(true); 
            const { run: result } = await executeCode(selectedLanguageData, sourceCode);
            console.log(result); 
            setOutput(result.output.split("\n"));
            result.stderr ? setIsError(true) : setIsError(false);
        } catch (error) {
            console.log(error); 
        } finally {
            setIsLoading(false); 
        }
    }

    return (
        <>
            <Navbar/>
            <div className="flex justify-center mt-[10px]">
                <div className="h-[1000px] w-[600px] ">
                    <div className="flex flex-col space-y-[10px]">
                        <div className="ml-auto">
                            <LanguageDropdown 
                                data={data}
                                selectedLanguageData={selectedLanguageData}
                                setSelectedLanguageData={setSelectedLanguageData}
                                onSelect={handleSelect}
                            />
                        </div>
                        <div className="shadow-md">
                            <CodeEditor selectedLanguageData={selectedLanguageData} code={code} setCode={setCode} editorRef={editorRef}/>
                        </div>
                        <div onClick={() => runCode()}>
                            <CodeRunButton/>
                        </div>
                        <Output output={output} isError={isError}/>
                    </div>
                </div>
            </div>
        </>
    )
}
```

@/app/api/Api.js
```js
import axios from "axios";

const API = axios.create({
    baseURL: "https://emkc.org/api/v2/piston"
})

export const executeCode = async(selectedLanguageData, sourceCode) => {
    const response = await API.post("/execute", {
        "language": selectedLanguageData.language, // required
        "version": selectedLanguageData.version, // required
        "files": [
            {
                "content": sourceCode // required
            }
        ],
    })

    return response.data;
}
```

CodeRunButton.js
```js
import { MdArrowRight } from "react-icons/md";

export default function CodeRunButton() {
    return (
        <>
            <button 
                className="w-[120px] h-[40px] p-2 border-2 border-solid rounded-md shadow-md
                text-green-600 text-lg font-bold hover:bg-green-600 hover:text-white flex items-center"
            >
                <div className="pl-[2px]">
                    <MdArrowRight size={30}/>
                </div>
                <div className="pl-[2px]">
                    Run
                </div>   
            </button>
        </>
    )
}
```

CodeEditor.js
```js
import { Editor } from "@monaco-editor/react";

export default function CodeEditor({selectedLanguageData, code, setCode, editorRef}) {
    const onMount = (editor) => {
        editorRef.current = editor;
        editor.focus();
    }

    return (
        <>
            <Editor
                 options={{
                    minimap: { enabled: false }
                }}
                height="500px"
                language={selectedLanguageData.language}              
                onMount={onMount}  
                value={code}   
                onChange={(code) => setCode(code)}         
            />
        </>
    )
}
```

Output.js
```js
export default function Output({output, isError}) {
    return (
        <>
            {
                output &&
                <div className="border-2 p-2">
                    <div className={isError ? "text-red-600 font-bold" : ""}>
                        {output.map(
                            (line, i) => <div key={i}>{line}</div>
                        )}
                    </div>
                </div>
            }
        </>
    )
}
```

CodeRunButton.js
```js
import { MdArrowRight } from "react-icons/md";

export default function CodeRunButton() {
    return (
        <>
            <button 
                className="w-[120px] h-[40px] p-2 border-2 border-solid rounded-md shadow-md
                text-green-600 text-lg font-bold hover:bg-green-600 hover:text-white flex items-center"
            >
                <div className="pl-[2px]">
                    <MdArrowRight size={30}/>
                </div>
                <div className="pl-[2px]">
                    Run
                </div>   
            </button>
        </>
    )
}
```

CodeEditor.js
```js
import { Editor } from "@monaco-editor/react";

export default function CodeEditor({selectedLanguageData, code, setCode, editorRef}) {
    const onMount = (editor) => {
        editorRef.current = editor;
        editor.focus();
    }

    return (
        <>
            <Editor
                 options={{
                    minimap: { enabled: false }
                }}
                height="500px"
                language={selectedLanguageData.language}              
                onMount={onMount}  
                value={code}   
                onChange={(code) => setCode(code)}         
            />
        </>
    )
}
```

Output.js
```js
export default function Output({output, isError}) {
    return (
        <>
            {
                output &&
                <div className="border-2 p-2">
                    <div className={isError ? "text-red-600 font-bold" : ""}>
                        {output.map(
                            (line, i) => <div key={i}>{line}</div>
                        )}
                    </div>
                </div>
            }
        </>
    )
}
```

## 참조1 https://kaderbiral26.medium.com/building-a-custom-dropdown-component-in-react-step-by-step-e12f4330fb58
## 참조2 https://github.com/nikitadev-yt/react-code-editor-app
