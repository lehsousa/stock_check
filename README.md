# Stock Check | IT Asset Inventory Reconciliation

**Python · Streamlit · Pandas · Lansweeper exports · IT Asset Management**

[English](#english) | [Português](#português)

## English

### Overview

Stock Check supports the physical verification of notebooks and other IT equipment against an Excel inventory exported from Lansweeper. It connects asset records with the equipment being checked, helping a support team identify discrepancies that need investigation.

Developed in partnership by **Leandro Sousa de Jesus** ([lehsousa](https://github.com/lehsousa)) and **Wagner** ([wagnerws](https://github.com/wagnerws)). This repository is a fork of [wagnerws/stock_check](https://github.com/wagnerws/stock_check); the fork relationship and shared contribution history are part of the project.

### Implemented workflow

1. Import an inventory spreadsheet and validate its required columns.
2. Enter or scan a serial number through the text input, including keyboard-style barcode readers.
3. Match the equipment by serial number or asset tag.
4. Normalize supported Portuguese and English equipment states.
5. Flag equipment found in stock whose inventory status is still active.
6. Review session progress, discrepancies and inventory distribution by model.
7. Export adjustment lists and scan history as Excel files; review locally saved session history.

The application integrates with **exported Lansweeper data**. It does not update Lansweeper automatically. SharePoint synchronization is not implemented in the current local-storage workflow, even though some service function names mention SharePoint.

### Technical design

- **Interface:** Streamlit components for upload, verification, reporting and history.
- **Data processing:** Pandas and OpenPyXL.
- **Business logic:** separate services for validation, comparison and reporting.
- **Persistence:** local JSON session files under `data/sessions/`.
- **Testing:** pytest modules covering import, comparison, validation, state normalization and report metrics.

The UI currently identifies itself as **v0.8.0**. Older planning documents may describe earlier milestones. The repository includes tests; no current passing-test or coverage percentage is claimed by this README.

### Run locally

Use Python 3.11+ and an isolated environment. From the repository root:

```powershell
git clone --branch dev https://github.com/lehsousa/stock_check.git
cd stock_check
python -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m streamlit run app/main.py
```

On macOS/Linux, use `.venv/bin/python` instead. Barcode-related packages may require platform-specific native libraries.

The Excel import expects `Serialnumber`, `State`, `Name` and `lastuser`. `Ativo` is optional; model/OS/type columns support additional inventory filtering. Use an `.xlsx` file compatible with the importer.

```powershell
.venv\Scripts\python -m pytest tests/unit/
```

### Scope and data

Use synthetic or appropriately anonymized inventories for public demonstrations. Imported files and saved sessions can contain user names, hostnames and asset identifiers. Review application-specific labels and access controls before deploying beyond a local environment.

The original repository describes this project as intended for internal use. No new open-source license is granted by this documentation update.

### Professional relevance

IT asset reconciliation, endpoint inventory quality, Service Desk tooling, Python automation and operational reporting. This project does not claim a Microsoft Intune or Microsoft Graph integration.

## Português

### Visão geral

O Stock Check apoia a conferência física de notebooks e equipamentos de TI usando uma planilha exportada do Lansweeper. A aplicação relaciona os registros do inventário aos equipamentos conferidos e destaca divergências para investigação pela equipe de suporte.

Projeto desenvolvido em parceria por **Leandro Sousa de Jesus e Wagner**. Este repositório mantém o vínculo de fork com [wagnerws/stock_check](https://github.com/wagnerws/stock_check).

### Funcionalidades implementadas

- Importação de Excel com validação de colunas.
- Conferência por número de série ou patrimônio, com entrada manual ou leitor que funciona como teclado.
- Normalização de estados em português e inglês.
- Identificação de equipamentos presentes no estoque que ainda constam como ativos.
- Indicadores de progresso e distribuição de equipamentos por modelo.
- Exportação de ajustes e histórico em Excel.
- Histórico de sessões salvo localmente em JSON.

A integração ocorre por **exportação de dados do Lansweeper**, sem alteração automática da ferramenta. A sincronização com SharePoint permanece fora do fluxo implementado.

### Execução e estrutura

Os comandos da seção em inglês instalam as dependências de `requirements.txt`, iniciam a aplicação e executam os testes unitários. A interface fica em `app/components/`; regras de negócio e processamento ficam em `app/services/`; os testes ficam em `tests/unit/`.

A interface informa **v0.8.0**. A documentação de planejamento pode conter marcos antigos. A existência de testes no repositório não representa uma execução ou cobertura atual certificada.

### Aplicação profissional

O projeto demonstra aplicação de Python à gestão de ativos de TI, qualidade de inventário, conferência de endpoints e apoio às operações de Service Desk. Demonstrações públicas devem usar dados fictícios ou anonimizados. O caráter de uso interno indicado na documentação anterior foi preservado.
