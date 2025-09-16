# Creating a Vite Web Component from Scratch
In the labs you started out with a prebuilt scaffold for developing your Web Components using Vite + Lit.  In this section you will learn the steps to create that same setup from scratch.

!!! note w50 "Prerequisites"
    - Node JS
    - Yarn
    - VS Code 
    - Recommended VS Code Extensions:  
        - runem.lit-plugin
        - lit.lit-snippets
        - bierner.lit-html 

### Scaffold Vite
> In a folder where you are comfortable developing (you can create a new folder), open a terminal  
> Enter the command: <copy>yarn create vite</copy>  
> Enter a hyphenated name for your project like my-demo  
> Select Lit  
> Select TypeScript
> cd into your new directory  
>
> ---

### Add additional packages
> In the terminal of your new directory 
> === "If you are going to use the Webex Contact Center SDK"  
    Enter the command: <copy>yarn add vite-plugin-node-polyfills @webex/contact-center@next --dev @types/minimatch concurrently</copy>  
>
>
> === "If you are **NOT** using the Webex SDK, but may use some additional node packages"  
    Enter the command: <copy>yarn add vite-plugin-node-polyfills --dev @types/minimatch concurrently</copy>  
>
> Start VS Code in the current directory using the command <copy>code .</copy>  
> Create a new file named: <copy>vite.config.ts</copy>  
> !!! note w50 "Add this code into your new vite.config.ts file"
    ```TS
    import { defineConfig } from "vite";
    import { nodePolyfills } from 'vite-plugin-node-polyfills'

    export default defineConfig({
        build:{
            rollupOptions:{
                output:{
                    entryFileNames:"[name].js",
                    chunkFileNames:"[name].js",
                    assetFileNames:"[name].[ext]"
                }
            }
        },
        plugins: [
        nodePolyfills({
        // Whether to polyfill `node:` protocol imports.
        protocolImports: true,
        }),
    ]
    })
    ```
> Save the file  
>
> ---

### Add Script to package.json so that you can test inside the Agent Desktop after initial development
> Open the package.json  
> In the scripts section, after preview, add a comma and this <copy>`"game": "concurrently \"vite build --watch\" \"vite preview\""`</copy>  
>
> ---


## Enjoy your coding!