# GridResourceMonitor

Desktop WPF application for monitoring and managing distributed renewable energy resources on a 12-slot grid, with real-time measurement updates over TCP.

## Features

- Manage energy resources (create, search/filter, delete)
- Place, move, remove, and connect resources on a visual grid
- Undo the latest action (`Ctrl + Z`)
- Built-in terminal for command-driven operations
- Real-time measurement ingestion via TCP listener (`port 25675`)
- Alarm state when resource value is outside the valid range (`1` to `5`)
- Measurement history graph (latest 5 readings per resource)
- In-app toast notifications for success/error feedback

## Tech Stack

- C# / .NET Framework 4.7.2
- WPF (MVVM pattern)
- NuGet packages:
  - Notification.Wpf
  - FontAwesome5
  - Microsoft.Xaml.Behaviors.Wpf
  - MVVMLight.Messaging

## Project Structure

- `/NetworkService/ViewModel` – UI logic (entities, display, graph, terminal)
- `/NetworkService/Services` – terminal command handling, logging, measurement processing/reading
- `/NetworkService/Persistance` – in-memory app state and undoable actions
- `/NetworkService/Model` – domain models and undo action classes
- `/NetworkService/Views` – XAML views

## Prerequisites

- Windows
- Visual Studio 2019+ with **.NET desktop development** workload
- .NET Framework 4.7.2 targeting pack

## Getting Started

1. Open `/home/runner/work/NetworkService/NetworkService/NetworkService.sln` in Visual Studio.
2. Restore NuGet packages.
3. Build and run the `NetworkService` project.

## Runtime Notes

- The app starts a TCP listener on `0.0.0.0:25675`.
- Expected server messages:
  - `Need object count` (app responds with current resource count)
  - `Entitet_<index>:<value>` (measurement update)
- Measurements are logged to `log.txt` and used by the graph page.

## Terminal Commands

Top-level:

- `help`
- `undo`
- `add "<resource name>" "<resource type>"`
- `delete <resource_id>`
- `grid help`

Grid subcommands:

- `grid put <resource_id> into <slot_index>`
- `grid move <from_slot_index> to <to_slot_index>`
- `grid remove <slot_index>`
- `grid connect <from_slot_index> to <to_slot_index>`

Many mutating commands request confirmation with `Y/N`.

## Keyboard Shortcuts

- `Ctrl + Z` → Undo last action
- `Ctrl + Tab` → Switch back to previous page
- `Alt + Left / Alt + Right` → Navigate between pages
- `Ctrl + Delete` → Close application

## Recommended GitHub About Section

**Description**

WPF SCADA-style desktop app for managing distributed renewable energy resources with real-time TCP measurement updates, visual grid mapping, and command terminal control.

**Topics (tags)**

`wpf`, `csharp`, `dotnet-framework`, `mvvm`, `scada`, `energy-monitoring`, `renewable-energy`, `tcp`, `desktop-app`, `data-visualization`
