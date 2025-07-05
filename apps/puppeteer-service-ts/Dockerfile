FROM node:20-slim

WORKDIR /app

# 安装 pnpm
RUN npm install -g pnpm

# 安装 chromium（arm64 兼容）和常用字体
RUN apt-get update && \
    apt-get install -y chromium fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst fonts-symbola fonts-noto fonts-freefont-ttf --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# 设置 Hero/Chromium 路径（如 Hero 支持）
ENV HERO_CHROMIUM_PATH="/usr/bin/chromium"

# 拷贝依赖文件
COPY ./package.json ./pnpm-lock.yaml ./

# 安装依赖
RUN pnpm install --frozen-lockfile

# 拷贝代码
COPY . .

# 安装 Playwright 浏览器依赖（如有 Playwright 需求）
RUN npx playwright install --with-deps chromium

# 构建
RUN pnpm run build

ARG PORT=3000
ENV PORT=${PORT}

EXPOSE ${PORT}

CMD ["pnpm", "start"]
