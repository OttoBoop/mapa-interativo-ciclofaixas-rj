# Mapa Interativo de Ciclofaixas do Rio de Janeiro

Mapa interativo da infraestrutura cicloviaria do Rio de Janeiro, com sistema de **reporte de problemas** direto no mapa.

**[Abrir o mapa ao vivo](https://ottoboop.github.io/mapa-interativo-ciclofaixas-rj/)**

---

## O que e este projeto?

Este projeto visualiza todas as ciclovias, ciclofaixas e vias compartilhadas do Rio de Janeiro usando dados do [OpenStreetMap](https://www.openstreetmap.org/). Alem da visualizacao, ele permite que qualquer pessoa **clique no mapa para reportar um problema** na infraestrutura cicloviaria.

### Funcionalidades do mapa

- **3 camadas de infraestrutura** (ligam/desligam individualmente):
  - Ciclovia Exclusiva (vermelho)
  - Ciclofaixa Dedicada (azul)
  - Via Compartilhada (laranja)

- **Sistema de reporte de problemas:**
  - Clique em qualquer ponto do mapa para abrir o formulario
  - Escolha a categoria: Buraco/Desnivel, Falta de Sinalizacao, Obstrucao, Trecho Perigoso, Iluminacao, Outro
  - Defina a severidade: Info, Baixo, Medio, Critico
  - Anexe fotos (multiplas)
  - Os dados ficam salvos no navegador (localStorage)

- **Exportar/Importar dados:**
  - Exporte seus reportes como arquivo JSON
  - Importe reportes de colegas para consolidar dados
  - Util para trabalho colaborativo em campo

## Como usar

### Opcao 1: Usar o mapa online (recomendado)

Acesse: **https://ottoboop.github.io/mapa-interativo-ciclofaixas-rj/**

1. Clique no mapa no local onde ha um problema
2. Preencha o formulario (categoria, descricao, severidade, fotos)
3. Clique em **Salvar**
4. O marcador aparece no mapa com a cor da severidade
5. Use **Exportar JSON** no painel inferior direito para salvar seus dados

### Opcao 2: Rodar os notebooks localmente

Se quiser modificar ou regenerar os mapas:

```bash
# Instalar dependencias
pip install osmnx geopandas folium

# Abrir o notebook
jupyter notebook notebooks/Mapa_problemas_ciclofaixas.ipynb
```

Os notebooks baixam os dados do OpenStreetMap automaticamente e geram os arquivos HTML.

## Estrutura do repositorio

```
├── index.html                              # Mapa com reporte de problemas (pagina principal)
├── mapa_interativo_ciclovias.html          # Mapa so de visualizacao (sem reporte)
├── notebooks/
│   ├── Mapinha_interativo_ciclofaixas.ipynb # Notebook: mapa basico
│   └── Mapa_problemas_ciclofaixas.ipynb    # Notebook: mapa com reporte de problemas
├── dados/
│   └── ciclovias_rj.geojson                # Cache dos dados do OpenStreetMap
└── README.md
```

## Tecnologias

| Tecnologia | Uso |
|---|---|
| [Python](https://python.org) | Linguagem principal dos notebooks |
| [OSMnx](https://osmnx.readthedocs.io/) | Download de dados do OpenStreetMap |
| [GeoPandas](https://geopandas.org/) | Manipulacao de dados geoespaciais |
| [Folium](https://python-visualization.github.io/folium/) | Geracao de mapas interativos (wrapper do Leaflet.js) |
| [Leaflet.js](https://leafletjs.com/) | Framework JavaScript para mapas interativos |
| JavaScript/HTML/CSS | Interface do formulario de reporte (injetado no mapa) |

## Niveis de severidade

| Severidade | Cor no mapa | Significado |
|---|---|---|
| Info | Azul | Sugestao de melhoria, observacao |
| Baixo | Verde | Problema menor, nao impede o uso |
| Medio | Laranja | Problema significativo, requer atencao |
| Critico | Vermelho | Perigo real, risco de acidente |

## Formato do JSON exportado

```json
{
  "versao": "1.0",
  "exportado_em": "2026-03-16T14:30:00",
  "total": 1,
  "problemas": [
    {
      "id": 1,
      "lat": -22.9068,
      "lng": -43.1729,
      "categoria": "Buraco/Desnivel",
      "descricao": "Buraco grande na ciclovia",
      "severidade": "Medio",
      "imagens": ["data:image/jpeg;base64,..."],
      "data_criacao": "2026-03-16T14:25:00"
    }
  ]
}
```

## Limitacoes

- As fotos sao comprimidas para 800px e JPEG 70% (para caber no localStorage)
- O localStorage tem limite de ~5-10 MB — suficiente para ~50-100 problemas com fotos
- Se o armazenamento encher, exporte os dados e use "Limpar Tudo"
- Os dados ficam salvos **por navegador** — se trocar de navegador ou computador, importe o JSON

## Fonte dos dados

Os dados de infraestrutura cicloviaria sao do [OpenStreetMap](https://www.openstreetmap.org/), baixados via [OSMnx](https://osmnx.readthedocs.io/). O OpenStreetMap e um projeto colaborativo de mapeamento — os dados refletem o que a comunidade mapeou ate o momento do download.

## Licenca

MIT
