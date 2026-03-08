# Stage 1: Build
FROM golang:alpine AS builder
WORKDIR /app

# คัดลอกไฟล์ที่จำเป็นและดาวน์โหลด dependencies
COPY go.mod go.sum ./
RUN go mod download

# คัดลอกโค้ดทั้งหมดและทำการ Build
COPY . .
RUN go build -o tracking-service main.go

# Stage 2: Run
FROM alpine:latest
WORKDIR /root/

# คัดลอกไฟล์ที่ Build เสร็จแล้วจาก Stage 1
COPY --from=builder /app/tracking-service .
# คัดลอกไฟล์ HTML สำหรับทดสอบ (ถ้ามี)
COPY --from=builder /app/tracker.html . 

EXPOSE 8081

# รัน Service
CMD ["./tracking-service"]