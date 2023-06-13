## 설치

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## WEB UI 접속

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## 비번셋업

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" 
```

## kustomization sample
```yaml
name: Develop Server Deploy CI

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - name: Checkout
        run: |
          echo "RELEASE_VERSION=latest" >> $GITHUB_ENV
          

      # 도커 이미지 빌드 & 푸시
      - name: Build & Push image
        id: build-image
        run: |
          echo "install & build"                     

      # kustomize 명령을 가져온다.
      - name: Setup Kustomize
        uses: imranismail/setup-kustomize@v1

      - name: Checkout kustomize repository
        uses: actions/checkout@v2
        with:
          # kubernetes 설정정보 저장소
          repository: dechocolate/esc-infra
          ref: main
          # 다른 저장소에 push 하려면 Personal Access Token이 필요.
          token: ${{ secrets.ACTION_TOKEN }}
          path: esc-infra

      # 새 이미지 버전으로 파일 수정
      - name: Update Kubernetes resources
        run: |
          cd esc-infra/charts/esc-server/
          kustomize edit set image esc-server=$ECR_REGISTRY/$ECR_REPOSITORY:$RELEASE_VERSION
          cat kustomization.yaml

      # 수정된 파일 commit & push
      - name: Commit files
        run: |
          cd esc-infra
          git config --global user.email "github-actions@github.com"
          git config --global user.name "github-actions"
          git commit -am "deploy: Update image tag"
          git push -u origin main

```