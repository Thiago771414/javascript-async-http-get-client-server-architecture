# JavaScript Async HTTP GET Client-Server Architecture

> A practical case study demonstrating how modern web applications retrieve data asynchronously using HTTP GET, XMLHttpRequest and async/await patterns.

![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)
![HTTP](https://img.shields.io/badge/Protocol-HTTP-blue?style=for-the-badge)
![AJAX](https://img.shields.io/badge/Pattern-AJAX-green?style=for-the-badge)
![Async](https://img.shields.io/badge/Async-await-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Case%20Study-black?style=for-the-badge)

---

## Overview

Modern applications constantly retrieve data from servers.

This project demonstrates how to:

- Perform asynchronous HTTP GET requests
- Fetch structured data (JSON)
- Process responses
- Update UI dynamically

---

## The Problem

Without async data fetching:

```text
Full page reloads
Blocking UI
Poor user experience
```

With async GET requests:

```text
Dynamic updates
Non-blocking UI
Better performance
```

## Architecture
```text
User Action (Click Button)
        ↓
JavaScript Event Handler
        ↓
HTTP GET Request
        ↓
Server / Resource (JSON)
        ↓
Response Processing
        ↓
UI Rendering
```

## Request Flow
```text
1. User triggers action
2. GET request is sent
3. Server returns JSON
4. Data is parsed
5. UI is updated dynamically
```

## Example: XMLHttpRequest
```js
function ajax() {
  const xhr = new XMLHttpRequest();

  xhr.open("GET", "dados.json");

  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if (xhr.status === 200) {
        const data = JSON.parse(xhr.responseText);

        document.getElementById("nome").innerText = data.nome;
        document.getElementById("idade").innerText = data.idade;

        const filhos = data.filhos
          .map(f => f.nome)
          .join(", ");

        document.getElementById("filhos").innerText = filhos;
      } else {
        console.warn("Erro na requisição");
      }
    }
  };

  xhr.send();
}
```
## Modern Approach: Async/Await + Fetch
```js
async function carregarDados() {
  try {
    const response = await fetch("dados.json");

    if (!response.ok) {
      throw new Error("Erro na requisição");
    }

    const data = await response.json();

    document.getElementById("nome").innerText = data.nome;
    document.getElementById("idade").innerText = data.idade;

    const filhos = data.filhos
      .map(f => f.nome)
      .join(", ");

    document.getElementById("filhos").innerText = filhos;

  } catch (error) {
    console.error(error);
  }
}
```

## Data Transformation Insight

```text
Raw JSON → Parsed Object → UI Mapping
```
## Example:

```js
data.filhos.map(f => f.nome)
```

| Feature | XMLHttpRequest | Fetch |
| :--- | :--- | :--- |
| **Syntax** | Verbose | Clean |
| **Promises** | No | Yes |
| **Async/Await** | No | Yes |
| **Modern Usage** | Legacy | Recommended |

## Architecture Insight
```text
Client = requests data
Server = provides data
JavaScript = transforms data
UI = displays data
```

## Real Engineering Use Cases
```text
Dashboards
User profiles
Analytics data
Product listings
API integrations
```

## Demo
## Layout Ajax

[![Assista ao vídeo do Ajax](https://github.com/Thiago771414/imagensProjetos/blob/main/slices/mobile/ajaxGet.png)](https://youtu.be/-PSPDSj0ew4)

*Clique na imagem acima para assistir à demonstração.*

---

## Performance Considerations
```text
Avoid redundant requests
Use caching strategies
Batch requests when possible
Lazy load data
```

## Common Mistakes

❌ Not handling errors
❌ Ignoring response status
❌ Blocking UI
❌ Mixing UI with data logic
❌ Not validating JSON

## Advanced Topics
```text
Caching (LocalStorage / IndexedDB)
Pagination
Debouncing requests
Retry strategies
Data normalization
```

## Summary

GET requests are the foundation of data-driven applications.
```text
Request = data retrieval
Response = data source
UI = data representation
```

## Author

Thiago Lima
Software Engineer | System Design | Data Fetching Architecture
