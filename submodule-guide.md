# Super-repo + Submodules Guide

## Cấu trúc

```
microservices-app/                     ← super-repo
├── .git/
├── .gitmodules                        ← track 2 submodules
├── .gitignore
├── submodule-guide.md                 ← file này
├── backend/                           ← submodule
│   ├── .git/
│   ├── services/
│   ├── libs/
│   ├── packages/
│   ├── docker-compose.yml
│   ├── package.json
│   └── ...
└── frontend/                          ← submodule
    ├── .git/
    ├── app/
    ├── src/
    ├── package.json
    └── ...
```

### Remote repos

| Repo       | URL                                                          |
| ---------- | ------------------------------------------------------------ |
| Super-repo | `leminhthe04/fpt-nodejs-01-nestjs-microservice-app`          |
| Backend    | `leminhthe04/fpt-nodejs-01-nestjs-microservice-app-backend`  |
| Frontend   | `leminhthe04/fpt-nodejs-01-nestjs-microservice-app-frontend` |

## Clone toàn bộ project

```bash
git clone --recurse-submodules https://github.com/leminhthe04/fpt-nodejs-01-nestjs-microservice-app.git
cd fpt-nodejs-01-nestjs-microservice-app
git submodule update --init --recursive
```

## Chỉ lấy backend/ (cho người làm backend)

```bash
git clone --recurse-submodules --single-branch \
  https://github.com/leminhthe04/fpt-nodejs-01-nestjs-microservice-app-backend.git
```

## Chỉ lấy frontend/ (cho người làm frontend)

```bash
git clone --recurse-submodules --single-branch \
  https://github.com/leminhthe04/fpt-nodejs-01-nestjs-microservice-app-frontend.git
```

## Workflow hàng ngày

### Update submodules lên phiên bản mới nhất

```bash
git submodule update --remote --merge
# hoặc pull từng cái riêng:
cd backend && git pull origin main && cd ..
cd frontend && git pull origin main && cd ..
```

### Commit thay đổi submodule trong super-repo

```bash
git add backend frontend
git commit -m "chore: update submodules to latest"
git push origin main
```

### Clone lần đầu (nếu quên --recurse-submodules)

```bash
git submodule update --init --recursive
```

## Lưu ý

| Hành động                | Làm ở super-repo                           | Làm ở submodule trực tiếp            |
| ------------------------ | ------------------------------------------ | ------------------------------------ |
| Sửa code backend         | ❌                                         | `cd backend && git add/commit/push`  |
| Sửa code frontend        | ❌                                         | `cd frontend && git add/commit/push` |
| Update submodule version | `git submodule update --remote`            | ❌                                   |
| Deploy                   | Mỗi submodule deploy độc lập (CI/CD riêng) |                                      |
