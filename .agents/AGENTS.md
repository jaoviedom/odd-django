# ODD Routing & Delegation Contract

1. **Authorize & Explore:** Mantén las consultas en modo solo lectura. Si la evidencia necesaria cabe en 1 lote paralelo (máximo 3 llamadas / ~10k tokens), explora e implementa directamente (inline).
2. **Cuándo delegar con `invoke_subagent`:**
   - Usa `explorer` cuando necesites mapear una zona amplia del repositorio sin llenar tu ventana de contexto.
   - Usa `worker` para delegar unidades de trabajo independientes o continuar sesiones largas sobre un documento `odd/tasks/<slug>.md`.
   - Usa `verify` para realizar una verificación independiente con contexto limpio en cambios de alto riesgo (seguridad, datos, contratos compartidos).
