# 🏷️ Auto Tagger

Automatically applies genre, decade, rating, language, and resolution tags to every movie and TV series in your Jellyfin library based on their metadata.

Works hand-in-hand with [Seasonal Visibility](https://github.com/jshafer813/Seasonal-Visibility) — Auto Tagger writes the tags, Seasonal Visibility uses them to show or hide content per user.

---

## ✨ Features

- Genre tags — maps Jellyfin genres to custom tags (e.g. `tag-action`, `tag-horror`)
- Decade tags — tags items by release year (e.g. `tag-80s`, `tag-90s`)
- Rating tags — tags items by official rating (e.g. `tag-rated-r`, `tag-rated-pg13`)
- Language tags — tags items by audio language (e.g. `tag-lang-english`, `tag-lang-japanese`)
- Resolution tags — tags items by video quality (e.g. `tag-hd`, `tag-fullhd`, `tag-4k`)
- Stale tag cleanup — removes old auto-applied tags before re-tagging when rules change
- Dry run preview — see exactly what would be tagged before committing
- Runs daily at 3am automatically, or manually from Scheduled Tasks

---

## 📦 Installation

1. Download `Jellyfin.Plugin.AutoTagger.dll` from the [Releases](https://github.com/jshafer813/Auto-Tagger/releases) page
2. Create a folder `plugins/AutoTagger` inside your Jellyfin data directory
3. Copy the DLL into that folder
4. Restart Jellyfin
5. Navigate to **Dashboard → Plugins → Auto Tagger** to configure

### Jellyfin data directory locations

| OS | Path |
|---|---|
| Linux | `/var/lib/jellyfin/plugins/AutoTagger/` |
| Docker | `/config/plugins/AutoTagger/` |
| Windows | `%APPDATA%\Jellyfin\plugins\AutoTagger\` |

---

## 🏷️ How It Works

Auto Tagger scans every Movie and Series in your library and applies tags based on their metadata:

- **Genre tags** — mapped via a configurable `Genre Name=tag-name` list
- **Decade tags** — based on `PremiereDate` year
- **Rating tags** — based on `OfficialRating` field (e.g. PG-13, TV-MA)
- **Language tags** — based on audio stream ISO 639 language codes
- **Resolution tags** — based on video stream height (720p, 1080p, 2160p)

Tags are plain Jellyfin tags and work anywhere tags are accepted — user policies, smart collections, filters, and Seasonal Visibility blocked tag rules.

---

## 🔗 Pairing with Seasonal Visibility

1. Run Auto Tagger to stamp tags onto your library
2. Open **Seasonal Visibility** and add a rule blocking e.g. `tag-horror` outside of October
3. Horror movies disappear for non-admin users outside of October — and reappear automatically

---

## ⚙️ Requirements

- Jellyfin **10.11.6+**
- .NET 9 (for building from source)

---

## 🔨 Building from source
```bash
dotnet build Jellyfin.Plugin.AutoTagger/Jellyfin.Plugin.AutoTagger.csproj \
    --configuration Release --output bin/Publish
```

---

## 📜 Changelog

- **v1.0.0** — Initial release: genre, decade, rating, language and resolution tagging with dry run preview and stale tag cleanup
