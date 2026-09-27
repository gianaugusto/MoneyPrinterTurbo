# Diretório de Testes do MoneyPrinterTurbo

Este diretório contém testes unitários para o projeto **MoneyPrinterTurbo**.

## Estrutura de Diretórios

- `services/`: testes unitários e de controlador por domínio
  - `test_task.py`: testes do pipeline de tarefas
  - `test_task_manager.py`: testes da fila em memória e Redis
  - `test_controller_*.py`: testes de API de controlador divididos por domínio
  - `test_video.py`, `test_voice.py`: testes de serviços de mídia
- `test_main.py`: teste do ponto de entrada da aplicação

## Executando Testes

A suíte de CI usa pytest, que também executa os testes existentes de `unittest.TestCase`:

```bash
# Executa todos os testes
uv run python -X utf8 -m pytest -q test

# Executa um arquivo de teste específico
uv run python -X utf8 -m pytest -q test/services/test_video.py

# Executa uma classe de teste específica
uv run python -X utf8 -m pytest -q test/services/test_video.py::TestVideoService

# Executa um método de teste específico
uv run python -X utf8 -m pytest -q test/services/test_video.py::TestVideoService::test_preprocess_video
```

Para executar a mesma verificação de cobertura de branch usada pela CI:

```bash
uv run python -X utf8 -m coverage run -m pytest -q test
uv run python -m coverage report
```

Testes de provedores ao vivo são ignorados por padrão. Para executar testes que possam chamar serviços externos de TTS ou LLM, defina `MPT_RUN_INTEGRATION_TESTS=1` e forneça as credenciais necessárias do provedor.

## Adicionando Novos Testes

Para adicionar testes para outros componentes, siga estas diretrizes:

1. Nomeie os arquivos como `test_<dominio>.py` e mantenha cada arquivo focado em um único domínio.
2. Divida suítes de controladores amplas em arquivos como `test_controller_video.py`.
3. Use funções pytest ou `unittest.TestCase`; o pytest coleta ambos.
4. Nomeie funções e métodos de teste com o prefixo `test_`.

## Recursos de Teste

Coloque qualquer arquivo de recurso necessário para testes no diretório `test/resources`.
