# openai

openai-proxy

- https://jihulab.com/devdo/worker-openai
- https://github.com/devdoz/worker-openai

## 布署教程

1. 注册 [CloudFlare 账号](https://www.cloudflare.com/)，并且设置 **Workers** 域名 (比如：`xxx.workers.dev`)
2. 安装 [Wrangler 命令行工具](https://developers.cloudflare.com/workers/wrangler/)。
   ```bash
    npm install -g wrangler
   ```
3. 登录 `Wrangler`（可能需要扶梯）：

   ```bash
   # 登录，可能登录不成功
   wrangler login

   # 若登录不成功，可能需要使用代理。
   # 每个命令行前，均需要加 HTTP_PROXY=http://localhost:20171
   HTTP_PROXY=http://localhost:20171 wrangler login
   ```

4. 拉取本项目：

   ```bash
   git clone https://jihulab.com/devdo/worker-openai.git
   ```

5. 修改 `wrangler.toml` 文件中的 `name`（openai）为服务名 `xxx`（访问域名为：`openai.xxx.workers.dev`）

6. 发布

   ```bash
    HTTP_PROXY=http://localhost:20171 wrangler publish
   ```

   发布成功将会显示对应的网址

   ```bash
    Proxy environment variables detected. We'll use your proxy for fetch requests.
   ⛅️ wrangler 2.13.0
   	--------------------
   	Total Upload: 0.66 KiB / gzip: 0.35 KiB
   	Uploaded openai (1.38 sec)
   	Published openai (4.55 sec)
   		https://openai.xxx.workers.dev
   	Current Deployment ID:  xxxx.xxxx.xxxx.xxxx
   ```

7. 使用过程中，把官方文档中的 https://api.openai.com 替换成 https://openai.xxx.workers.dev 即可。

   比如：
   `https://api.openai.com/v1/chat/completions` 修改为 `https://openai.xxx.workers.dev/v1/chat/completions`。

   **由于某些原因，`workers.dev` 可能无法正常访问，建议绑定自有域名。**

8. 绑定域名

   在 Cloudflare Workers 的管理界面中，点击 `Triggers` 选项卡，然后点击 `Custom Domians` 中的 `Add Custom Domain` 按钮以绑定域名。

## Template: worker-typescript

- https://github.com/cloudflare/workers-sdk/tree/main/templates

```bash
# full repository clone
$ git clone --depth 1 https://github.com/cloudflare/workers-sdk

# copy the "worker-typescript" example to "my-project" directory
$ cp -rf workers-sdk/templates/worker-typescript my-project

# setup & begin development
$ cd my-project && npm install && npm run dev
```

```bash
HTTP_PROXY=http://localhost:20171 wrangler publish
```
