# [中文文档](README-zh_CN.md)

# vite-plugin-mkcert

Use mkcert to provide certificate support for vite https development services.

## When should I use this plugin

1. When you want to use `http/2` to solve the concurrency limit of vite http dev server requests, you find that the browser cache is invalid [#2725](https://github.com/vitejs/vite/issues/2725).
2. I have obsessive-compulsive disorder, and I hope that the browser will not show annoying https certificate errors.

## Effect

<details>
   <summary>View</summary>
   
   ![localhost](docs/assets/screenshot/localhost.png)

   ![127.0.0.1](docs/assets/screenshot/127.0.0.1.png)

   ![localhost](docs/assets/screenshot/localip.png)
</details>

## Quick start

1. Installation dependencies

```sh
yarn add vite-plugin-mkcert -D
```

2. Configure vite

```ts
import {defineConfig} from'vite'
import mkcert from'vite-plugin-mkcert'

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    https: true
  },
  plugins: [mkcert()]
})
```

## Parameters
### force

Whether to force generate.
### autoUpgrade

Whether to automatically upgrade `mkcert`.

### source

Specify the download source of `mkcert`, domestic users can set it to `coding` to download from the coding.net mirror, or provide a custom [BaseSource](plugin/mkcert/Source.ts).

### mkcertPath

If the network is restricted, you can specify a local `mkcert` file instead of downloading from the network.

### hosts

Custom hosts, default value is `localhost` + `local ip addrs`.

## Display the debugging information of the plug-in

Set the environment variable `DEBUG`=`vite:plugin:mkcert`

## CHANGELOG

[CHANGELOG](CHANGELOG.md)

## Principle

Use [mkcert](https://github.com/FiloSottile/mkcert) to install the local `CA` certificate and generate it for [server.https](https://vitejs.bootcss.com/config/#server-https) Server certificate.

## Friendly reminder

1. `mkcert` save directory: [PLUGIN_DATA_DIR](plugin/lib/constant.ts)
2. Uninstall the `CA` certificate: `mkcert uninstall`

## Thanks

- [mkcert](https://github.com/FiloSottile/mkcert)
- [daquinoaldo/https-localhost](https://github.com/daquinoaldo/https-localhost)