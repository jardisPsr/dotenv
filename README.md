# JardisPsr DotEnv Interface

[![PHP Version](https://img.shields.io/badge/php-%3E%3D8.2-blue.svg)](https://php.net/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Eine **Contract-Only PHP-Bibliothek**, die das `DotEnvInterface` für Domain-Driven-Design-Anwendungen definiert.

## Übersicht

Dieses Paket stellt ausschließlich ein Interface bereit – **keine Implementierung**. Es dient als Abstraktionsschicht für DotEnv-Funktionalität und unterscheidet zwischen:

- **Öffentlichen Umgebungsvariablen** (systemweit, geladen in `$_ENV`)
- **Privaten Umgebungsvariablen** (anwendungsspezifisch, als Array zurückgegeben)

## Installation

```bash
composer require jardispsr/dotenv
```

## Interface

```php
namespace JardisPsr\DotEnv;

interface DotEnvInterface
{
    /**
     * Lädt öffentliche Umgebungsvariablen in die Systemumgebung ($_ENV, getenv)
     *
     * @param string $pathToEnvFiles Pfad zum Verzeichnis mit .env-Dateien
     * @throws Exception
     */
    public function loadPublic(string $pathToEnvFiles): void;

    /**
     * Lädt und gibt private Umgebungsvariablen als Array zurück
     *
     * @param string $pathToEnvFiles Pfad zum Verzeichnis mit .env-Dateien
     * @return array<string, mixed>|null
     * @throws Exception
     */
    public function loadPrivate(string $pathToEnvFiles): mixed;
}
```

## Verwendung

Implementieren Sie das Interface in Ihrer eigenen Klasse:

```php
use JardisPsr\DotEnv\DotEnvInterface;

class MeinDotEnv implements DotEnvInterface
{
    public function loadPublic(string $pathToEnvFiles): void
    {
        // Implementierung zum Laden öffentlicher Variablen
    }

    public function loadPrivate(string $pathToEnvFiles): mixed
    {
        // Implementierung zum Laden privater Variablen
        return $privateVars;
    }
}
```

## Entwicklung

Das Projekt nutzt Docker für alle Entwicklungsaufgaben. **Führen Sie niemals Composer-, PHPStan- oder PHPCS-Befehle direkt auf dem Host aus** – verwenden Sie immer die Makefile-Targets.

### Voraussetzungen

- Docker
- Docker Compose
- Make

### Verfügbare Befehle

```bash
# Abhängigkeiten installieren
make install

# Abhängigkeiten aktualisieren
make update

# Autoloader neu generieren
make autoload

# Code-Style prüfen (PSR-12)
make phpcs

# Statische Analyse durchführen (PHPStan Level 8)
make phpstan

# Container-Shell öffnen
make shell

# Docker-Ressourcen aufräumen
make remove
```

## Qualitätsstandards

### PHP_CodeSniffer
- **Standard**: PSR-12
- **Zeilenlänge**: 120 (Limit), 150 (absolutes Limit)
- Strict Types erforderlich: `declare(strict_types=1);`

### PHPStan
- **Level**: 8 (maximale Strenge)
- **Analysierte Pfade**: `src/`

### Pre-Commit Hook

Nach der Installation wird automatisch ein Git Pre-Commit Hook eingerichtet, der:

1. Branch-Namen validiert: `(feature|fix|hotfix)/{1-7 digits}_{description}` oder `:{7-40 hex chars}`
2. Git-Benutzernamen validiert
3. PHPCS auf gestagte PHP-Dateien ausführt
4. Commits bei Fehlern blockiert

## PHP-Anforderungen

- **Minimum**: PHP 8.2
- **Empfohlen**: PHP 8.3

## Versionierung

Dieses Projekt folgt [Semantic Versioning](https://semver.org/). Da es sich um einen Contract handelt, sind Breaking Changes selten und erscheinen nur in Major-Versionen.

## Lizenz

MIT License - siehe [LICENSE](LICENSE) für Details.

## Support

- **Issues**: [GitHub Issues](https://github.com/JardisPsr/detenv/issues)
- **E-Mail**: jardisCore@headgent.dev

## Autoren

Jardis Core Development Team
