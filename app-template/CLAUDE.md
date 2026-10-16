# Zasady pracy w tym repo

- Pracuj na krótkich gałęziach `feat/...` lub `fix/...` i otwieraj PR do `main`. Nie pushuj bezpośrednio do `main`.
- Przed PR uruchom lokalnie `npm test` i `npx playwright test`.
- Apka nasłuchuje na porcie 3000 i bierze konfigurację ze zmiennych środowiskowych (`DATABASE_URL`, `APP_ENV`).
- Merge do `main` wdraża na stage automatycznie. Nie twórz tagów `v*` i nie uruchamiaj workflow Release ręcznie: wydanie na prod robi właściciel repo.
- Wspólne CI, release i stack Portainera są w repo `infra`. Zmiany w nich proponuj tam osobnym PR.
