# Complete Project Structure

Below is the exact directory and file blueprint of the private production repository (`164` files across `7` numbered layers). Source files are kept private; this map documents how every module, package, tool, and asset is organized.

```text
asset-roblox/
├── .github/
│   └── workflows/
│       └── validate.yml                          # Automated CI running validate_luau.py
├── .gitignore
├── README.md                                     # Engineering documentation
├── default.project.json                          # Auto-generated Rojo project mapping
│
├── 01_Assets_Luau_Universels/                    # 21 Modular Systems · 67 --!strict Luau Scripts
│   ├── Core_Systemes_De_Base/
│   │   ├── UniversalDataStore/                   # Config, DataStoreBootstrap.server, UniversalDataStore, README
│   │   ├── UniversalGamepassShop/                # Config, ShopService, Server, Client, README
│   │   ├── UniversalNotification/                # Config, NotificationService, Server, Client, README
│   │   ├── UniversalSoundVFX/                    # SoundDatabase, SoundPlayer, Server, Client, README
│   │   └── UniversalThemeEngine/                 # Config, Top10Palettes, ThemeStyler, README
│   │
│   ├── Gameplay_Mecaniques/
│   │   ├── UniversalBoosts/                      # Config, BoostService, Server, Client, README
│   │   ├── UniversalCaseOpening/                 # Config, CaseOpeningService, Server, Client, README
│   │   ├── UniversalCheckpoints/                 # Config, Server, README
│   │   ├── UniversalCollectible/                 # Config, Server, Client, README
│   │   ├── UniversalFirst20MinHook/              # Config, Server, Client, README
│   │   ├── UniversalMultiDayRetention/           # Config, RetentionService, Server, Client, README
│   │   ├── UniversalPadsHazards/                 # Config, Server, README
│   │   ├── UniversalPlaytimeGifts/               # Config, Server, Client, README
│   │   ├── UniversalSprintStamina/               # Config, Server, Client, README
│   │   ├── UniversalTycoon/                      # Config, ProgressionCurve, TycoonService, Server, Client, README
│   │   └── UniversalVisualTutorial/              # Config, Server, Client, README
│   │
│   └── Monde_Et_Environnement/
│       ├── Universal3DModelKit/                  # Procedural 3D model factory & configs
│       ├── UniversalDayNightCycle/               # Config, Server, README
│       ├── UniversalDoor/                        # Config, Server, README
│       ├── UniversalGlobalLeaderboard/           # Config, Server, README
│       └── UniversalTeleporter/                  # Config, Server, Client, README
│
├── 02_Packages_Studio_Prets_A_Glisser/           # 27 Auto-Compiled .rbxmx Studio Packages
│   ├── AllUniversalAssets.rbxmx                  # Unified 21-system bundle with MasterAutoDeploy
│   ├── Universal*.rbxmx                          # 21 standalone drag-and-drop system packages
│   └── Modeles_3D/
│       └── All_16_Universal_3DModels.rbxmx       # Pre-tagged procedural 3D model packs
│
├── 03_Kits_UI_Importes_RBXM/                     # 9 Cataloged UI Kits (.rbxm + README sheets)
│   ├── Admin_UIverse_Admin_V1/
│   ├── Boutique_UIverse_Limited_Store/
│   ├── Bouton_Square_Shine_Button/
│   ├── Classement_UIverse_Top_Donators/
│   ├── HUD_The_HUD_Kit/
│   ├── HUD_UIverse_Ready_To_Use/
│   ├── Joueurs_UIverse_Nametag_Kit/
│   ├── Menu_UIverse_Main_Menu/
│   └── Progression_UIverse_Skill_Tree/
│
├── 04_Documentation/                             # Guides, Audits & Visual Maps
│   ├── AUDIT_COMPLET_PROJET.md                   # 3-sprint technical & security audit report
│   ├── CREATE_ASSET_GUIDE.md                     # Developer onboarding & module creation guide
│   ├── MAP_VISUELLE_FOLDER_ASSETS.png            # High-res visual architecture map
│   └── PALETTE_TOP10_ROBLOX_COULEURS.png         # Top 10 color & gradient reference sheet
│
├── 05_Outils_Developpement/                      # 6 Python CLI Automation Tools
│   ├── new_asset.py                              # Module scaffolder
│   ├── build_rbxmx.py                            # XML .rbxmx compiler & Rojo updater
│   ├── build_3d_models_rbxmx.py                  # 3D model packager
│   ├── validate_luau.py                          # Static analysis, security & XML/JSON auditor
│   ├── generate_folder_map.py                    # Visual folder map generator
│   └── generate_palette_chart.py                 # Theme palette chart generator
│
├── 06_Prompts_Maps_Roblox/                       # 8 Low-Poly Map Blueprints + Template
│   ├── 00_TEMPLATE_PROMPT_MAP_ROBLOX.md
│   ├── 01_Tycoon_Island_Neon_Factory.md
│   ├── 02_Simulator_Hub_Floating_Islands.md
│   ├── 03_Obby_Sky_Parkour_Tower.md
│   ├── 04_Mythology_Olympus_Arena.md
│   ├── 05_Cyberpunk_City_Lobby.md
│   ├── 06_Medieval_Fantasy_Village.md
│   ├── 07_Space_Station_SciFi_Base.md
│   ├── 08_Tropical_Pirate_Cove.md
│   └── README.md
│
└── 07_Modeles_3D_Blender/                        # 16 Procedural 3D Models & Blender Pipeline
    ├── Blender_Scripts_BPY/
    │   └── build_all_glb_in_blender.py           # Headless Blender (bpy) mesh generator
    ├── Previews/
    │   ├── Pack1_Tycoon_3D.jpg
    │   ├── Pack2_CaseOpening_3D.jpg
    │   ├── Pack3_World_3D.jpg
    │   └── Pack4_Collectibles_3D.jpg
    ├── Prompts_3D_GLB/
    │   └── ALL_4_PACKS_PROMPTS_GLB.md
    └── README.md
```
