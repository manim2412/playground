# [nextjs official dynamic routes](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes)
# [Next.js 15 Tutorial - 7 - Dynamic Routes](https://www.youtube.com/watch?v=k9g6aVLH3p4&list=PLC3y8-rFHvwhIEc4I4YsRz5C7GOBnxSJY&index=7)
# [Next.js 15 Tutorial - 8 - Nested Dynamic Routes](https://www.youtube.com/watch?v=edrJf0GKfAI&list=PLC3y8-rFHvwhIEc4I4YsRz5C7GOBnxSJY&index=8)
# [Next.js 15 Tutorial - 9 - Catch all Segments](https://www.youtube.com/watch?v=d46hLIg1B3Q&list=PLC3y8-rFHvwhIEc4I4YsRz5C7GOBnxSJY&index=9)

src/app/problems/[problemId]/page.js
```js
export default async function Page({ params }) {
    const problemId = (await params).problemId; 
    console.log(params);
    console.log(problemId); 
    return (
        <>
            <div>
                problemId : {problemId}
            </div>
        </>
    )
}
```

src/app/problems/[problemId]/test/[testId]/page.js
```js
export default async function Page({ params }) {
    const { problemId, testId } = await params;
    return (
        <>
            <div>
                problemId : {problemId}
            </div>
            <div>
                testId : {testId}
            </div>
        </>
    )
}
```

src/app/docs/[...slug]/page.js
```js
export default async function Docs({ params }) {
    const { slug } = await params;

    if (slug?.length === 2) {
        return <h1>{slug[0]} {slug[1]}</h1>
    }
    return <h1>slug length is not 2</h1>
}
```
