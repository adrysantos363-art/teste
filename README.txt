TH IMPORTS V3 — GITHUB + FIREBASE MULTI-APARELHO

ESTA VERSÃO CORRIGE:
- Layout responsivo para celular.
- Catálogo público sincronizado com Firestore.
- O celular não depende do localStorage do computador.
- Alterações de preço/produto feitas pelo administrador são gravadas no Firestore.
- Outros aparelhos consultam o Firestore automaticamente a cada 5 segundos.
- Login administrativo usando Firebase Authentication.
- Exclusão de produto também remove do Firestore.

COMO PUBLICAR NO GITHUB PAGES
1. Extraia este ZIP.
2. Envie TODOS os arquivos para a raiz do repositório.
3. Mantenha a pasta assets.
4. No GitHub: Settings > Pages > Deploy from a branch > main > / (root).
5. Abra o endereço https://SEUUSUARIO.github.io/SEUREPOSITORIO/ no celular.

FIREBASE
Projeto configurado como referência pública:
projectId: thimports-1ce81

Para EDITAR produtos:
1. Abra o Painel admin.
2. Entre na aba Configurações.
3. Cole a configuração do seu app Web Firebase (apiKey, authDomain, projectId, storageBucket, messagingSenderId e appId).
4. Salve e conecte.
5. Entre com a conta criada no Firebase Authentication.
6. A conta administrativa precisa ter UID:
DqPq8jyUcNOfWrHYFWgssKHgCh93

FIRESTORE
Para o catálogo público aparecer em todos os aparelhos, a coleção products precisa permitir leitura pública.
Para gravação, mantenha a regra restrita ao UID do administrador.

Regra sugerida:
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /products/{productId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == "DqPq8jyUcNOfWrHYFWgssKHgCh93";
    }
    match /store/{documentId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == "DqPq8jyUcNOfWrHYFWgssKHgCh93";
    }
  }
}

IMPORTANTE
- Não coloque secret key de gateway no HTML.
- O ZIP usa imagens externas para alguns produtos/hero; o site precisa de internet para essas imagens.
- Se a leitura pública do Firestore estiver bloqueada, o catálogo não poderá ser sincronizado no celular.
