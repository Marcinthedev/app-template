<NAZWA APKI>
<Jedno zdanie: co robi apka i dla kogo.>
  
Stack: Node 22, TypeScript, <framework, np. Next.js>, <baza, np. PostgreSQL przez Prisma>, Playwright do e2e.
Komendy
`npm run dev`: serwer deweloperski na porcie 3000
`npm run lint`, `npm run typecheck`: muszą przechodzić bez błędów
`npm test`: testy jednostkowe
`npm run test:e2e`: Playwright (`BASE_URL` zmienia cel, domyślnie `http://localhost:3000`)
Mapa kodu
<Uzupełnij po pierwszych tygodniach albo poproś Claude'a o propozycję, np.:>
`src/app/`: routing i strony
`src/domain/`: logika biznesowa, bez zależności od frameworka
`src/infra/`: baza, zewnętrzne API
`tests/e2e/`: scenariusze Playwright
Słownik pojęć domenowych i decyzje architektoniczne prowadzi skill `domain-modeling` (pliki tworzy `/setup-matt-pocock-skills`).
Jak pracujemy
Proces pochodzi z mattpocock/skills (plugin włączony w `.claude/settings.json`).
Uzgodnij, zanim zaczniesz. Przy każdej nietrywialnej zmianie zacznij od `grilling`: zadawaj pytania z rekomendowaną odpowiedzią, aż obie strony rozumieją to samo. Fakty sprawdzaj sam, decyzje zostaw właścicielowi.
Większa funkcja: `/to-spec`, potem `/to-tickets` (issues na GitHubie), potem `/implement` dla kolejnych ticketów.
Implementacja przez `tdd`: najpierw czerwony test przez publiczny interfejs, potem minimalny kod. Jedna pionowa warstwa na raz.
Błąd: `diagnosing-bugs`. Najpierw test, który odtwarza błąd, dopiero potem poprawka.
Przed commitem skill `verify` (lint, typecheck, testy, e2e). Nie commituj na czerwono.
Pull request: skill `pr` do opisu, `code-review` przed oznaczeniem jako gotowy. Jeden PR to jedna zmiana.
Po merge'u: skill `stage-check` sprawdza deploy na stage.
Na koniec większej sesji: `/retro`, żeby poprawić ten plik, skille i narzędzia.
Definicja „gotowe”
[ ] Testy opisują zachowanie, nie implementację; nowa logika ma test, błąd ma test regresji
[ ] `verify` przechodzi lokalnie, CI na PR jest zielone
[ ] Zmiany w schemacie bazy mają migrację, która działa na kopii danych stage
[ ] Nowe zmienne środowiskowe są opisane w `.env.example` i w sekcji „Środowiska”
[ ] Opis PR mówi, co widzi użytkownik przed i po zmianie, oraz jak to cofnąć
Konwencje
TypeScript `strict`, bez `any` i bez `@ts-ignore` bez komentarza „dlaczego”
Walidacja danych na granicach systemu (API, formularze, zmienne środowiskowe), wewnątrz ufamy typom
Konfiguracja tylko ze zmiennych środowiskowych, nigdy zahardkodowane adresy ani sekrety
Commity w stylu Conventional Commits (`feat:`, `fix:`, `refactor:`, `test:`, `chore:`)
Gałęzie `feat/<krótki-opis>` lub `fix/<krótki-opis>`, zawsze PR do `main`
Środowiska
Środowisko	Adres	Jak trafia tam kod
dev	`http://localhost:3000` w stacji Claude'a	`npm run dev`
stage	`<adres stage>`	automatycznie po merge'u do `main`
prod	`<adres prod>`	tag `v*` tworzony wyłącznie przez właściciela
Zmienne: `DATABASE_URL`, `APP_ENV` (`stage` lub `prod`), <inne>.
Granice
Nigdy nie pushuj do `main`, nie twórz tagów `v*`, nie uruchamiaj workflow Release i nie twórz release'ów.
Nie czytaj ani nie zmieniaj plików `.env*` poza `.env.example`.
Nie wyłączaj testów ani reguł lintera, żeby przeszło CI. Jeśli test jest zły, napisz to w PR.
Wspólne CI, release i stack Portainera są w repo `infra`. Zmiany tam proponuj osobnym PR.
Gdy nie wiesz, co jest właściwym zachowaniem, zapytaj zamiast zgadywać.
