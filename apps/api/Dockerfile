FROM node:20-slim AS base

# 设置工作目录
WORKDIR /app

# 安装 pnpm
RUN npm install -g pnpm

# 安装 chromium（arm64 兼容）
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

# 构建
RUN pnpm run build

# 设置端口
ARG PORT=3000
ENV PORT=${PORT}
EXPOSE ${PORT}

# 启动应用
CMD ["pnpm", "start"]
