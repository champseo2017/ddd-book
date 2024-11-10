# syntax=docker/dockerfile:1

# Comments are provided throughout this file to help you get started.
# If you need more help, visit the Dockerfile reference guide at
# https://docs.docker.com/go/dockerfile-reference/

# กำหนดเวอร์ชั่นของ Node.js ที่จะใช้
ARG NODE_VERSION=20.8.0

# ใช้ image ของ Node.js เวอร์ชั่นที่กำหนด แบบ alpine (เป็น Linux ขนาดเล็ก)
FROM node:${NODE_VERSION}-alpine

# ตั้งค่าให้รันในโหมด production
ENV NODE_ENV production

# กำหนดโฟลเดอร์ที่จะทำงานใน container
WORKDIR /usr/src/app

# ติดตั้งแพ็คเกจที่จำเป็น
# --mount=type=bind คือการเชื่อมไฟล์จากเครื่องเราเข้าไปใน container
# --mount=type=cache คือการเก็บข้อมูลไว้ใช้ซ้ำ
# npm ci --omit=dev คือติดตั้งแพ็คเกจเฉพาะที่ใช้จริง ไม่รวมที่ใช้ตอนพัฒนา
RUN --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    --mount=type=cache,target=/root/.npm \
    npm ci --omit=dev

# สลับไปใช้ user ชื่อ node เพื่อความปลอดภัย
USER node

# คัดลอกไฟล์ทั้งหมดเข้าไปใน container
COPY . .

# บอกว่าแอพจะใช้พอร์ต 8080
EXPOSE 8080

# คำสั่งที่จะรันตอน start container
CMD node app.js
