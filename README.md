<p>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="profile/hecian-lc_oscuro.svg">
    <img src="profile/hecian-lc_claro.svg" alt="HECIAN LC" height="28">
  </picture>
</p>

# hecian-lc/.github

Lo común a todos los repos de la organización: workflows reutilizables de CI/CD, plantillas de issues y PR, política de seguridad y la portada de la organización.

## Workflows reutilizables

Se llaman desde cualquier repo de la organización con `uses: hecian-lc/.github/.github/workflows/<archivo>@v1`. Cada archivo explica arriba cómo usarlo.

| Workflow | Qué hace |
|---|---|
| [`ci-node.yml`](.github/workflows/ci-node.yml) | `npm ci`, lint, build y tests de una carpeta. Lo que el `package.json` no tiene, lo saltea |
| [`ci-python.yml`](.github/workflows/ci-python.yml) | Instala, corre ruff si está configurado y pytest si hay tests |
| [`seguridad.yml`](.github/workflows/seguridad.yml) | gitleaks sobre todo el historial (binario verificado), `npm audit` high+ de producción y semgrep opcional |
| [`release-docker.yml`](.github/workflows/release-docker.yml) | Imágenes amd64 y arm64 en `ghcr.io/hecian-lc/<repo>-<servicio>`, con `:latest` solo en versiones estables |
| [`marca.yml`](.github/workflows/marca.yml) | Licencia propietaria, `package.json` con `UNLICENSED` y `private`, firma en el README. Con `estricto: false` solo avisa |
| [`dependabot-automerge.yml`](.github/workflows/dependabot-automerge.yml) | Fusiona los PR de Dependabot de parches y menores cuando la CI pasó; los mayores quedan para revisión |

Para los repos que usan un runner propio, pasar `runner: ${{ vars.CI_RUNNER || 'ubuntu-latest' }}`.

### Versiones

Los repos apuntan a la etiqueta `v1`, que se mueve con cada cambio compatible. Un cambio que rompa la forma de llamarlos sale como `v2`, y `v1` queda donde estaba.

## Para un repo nuevo

1. En el repo: **Actions → New workflow → CI HECIAN LC** (sale de [`workflow-templates/`](workflow-templates/)).
2. Copiar [`plantillas/dependabot.yml`](plantillas/dependabot.yml) a `.github/dependabot.yml`.
3. Licencia, README y firma: [`hecian-lc/marca`](https://github.com/hecian-lc/marca), `plantillas/ESTANDAR.md` (privado).
4. Proteger la rama principal: PR obligatorio y los checks de CI requeridos.

## Plantillas por defecto

[`ISSUE_TEMPLATE/`](ISSUE_TEMPLATE/) (falla y mejora), [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) y [`SECURITY.md`](SECURITY.md) valen para todo repo de la organización que no tenga los suyos.

---

© 2026 HECIAN LC. Todos los derechos reservados.
