# [Next.js 15 Tutorial - 10 - Not Found Page](https://www.youtube.com/watch?v=GCipVDqBD3k&list=PLC3y8-rFHvwhIEc4I4YsRz5C7GOBnxSJY&index=10)

src/app/not-found.js
```js
export default function NotFound() {
    return (
        <>
            <h1>Page Not Found</h1>
        </>
    )
}
```

src/app/problems/[problemId]/not-found.js
```js
export default function NotFound() {
    return (
        <>
            Problem Not Found
        </>
    )
}
```

src/app/problems/[problemId]/page.js
```js
import NotFound from "@/app/not-found";
import { notFound } from "next/navigation";

export default async function Page({ params }) {
    const problemId = (await params).problemId; 
    console.log(params);
    console.log(problemId); 

    if (problemId > 100 && problemId<200) {
        return (
            <>
                <NotFound/>
            </>
        )
    } else if (problemId >= 200) {
        notFound();
    }

    return (
        <>
            <div>
                problemId : {problemId}
            </div>
        </>
    )
}
```
