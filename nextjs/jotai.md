# https://jotai.org/
## 1. 설치 
`npm install jotai`

## 2. app router 설정
/app/layout.js
```js
'use client'

import { Provider } from 'jotai'

export const Providers = ({ children }) => {
  return (
    <Provider>
      {children}
    </Provider>
  )
}


// ./app/layout.js
import { Providers } from '../components/providers'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <Providers>
          {children}
        </Providers>
      </body>
    </html>
  )
}
```
