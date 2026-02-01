# versioning.kt

## Přehled

Tento Kotlin soubor obsahuje rozšiřující funkce (extension functions) pro Gradle `Project`, které slouží k automatickému
generování verze projektu na základě Git repozitáře.

## Umístění

`api/buildSrc/src/main/kotlin/versioning.kt` (v rámci build logiky)

## Funkce

### `Project.gitHash(): String`

Získá aktuální zkrácený hash commitu (HEAD).

- Používá příkaz: `git rev-parse --verify HEAD`
- Pokud selže, vrací pomlčku `-`.

### `Project.gitClean(): Boolean`

Zjistí, zda je pracovní adresář čistý (neobsahuje nekommitované změny).

- Používá příkazy: `git update-index --refresh` a `git diff-index HEAD --`.

### `Project.gitVersion(): String`

Vygeneruje verzovací řetězec na základě tagů, commitů a větve.
**Logika:**

1. Získá poslední git tag (např. `v1.0`). Pokud není, použije `0.0`.
2. Spočítá počet commitů od posledního tagu do HEAD.
3. Získá název aktuální větve.
4. Sestaví verzi ve formátu: `verze[-větev][-commitů][-dirty]`
    - Pokud je větev `master` nebo prázdná, část s větví se vynechá.
    - Pokud je počet commitů 0, část s počtem commitů se vynechá.
    - Pokud repo není čisté (`gitClean()` vrací false), přidá se přípona `-dirty`.

### `Project.runCommand(cmd: String, fallback: String? = null): String`

Privátní pomocná funkce pro spouštění shell příkazů.

- Spustí příkaz v adresáři projektu.
- Čeká na dokončení (timeout 10s).
- Pokud příkaz skončí s exit kódem 0, vrátí jeho stdout.
- Pokud příkaz selže a je poskytnut `fallback`, vrátí fallback. Jinak vyhodí `IOException`.
