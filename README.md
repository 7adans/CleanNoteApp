# 📝 CleanNoteApp: Kotlin + Jetpack Compose with Clean Architecture

**A notes app for Android built with Clean Architecture, MVVM and Hilt. Each layer can be replaced or tested on its own, from the Room database to the Compose UI.**

## ✨ Features

- Add, list and delete notes, persisted locally with **Room**
- Configurable ordering (`NoteOrder` + `OrderType`), ascending or descending
- **Undo delete**: restore the last removed note
- Reactive data layer: notes are exposed as a `Flow` from Room

## 🧱 Architecture

```
feature_note/
├── domain/        # Note model, INoteRepository contract, use cases, ordering rules
│   └── use_cases/ # GetNotes · AddNote · DeleteNote, grouped in NoteUseCase
├── data/          # Room NoteDao + NoteDatabase, NoteRepository implementation
└── presentation/  # NotesViewModel (MVVM) · NotesState · NotesEvent
di/AppModule.kt    # Hilt: database, repository and use cases as singletons
```

- **Dependency inversion:** the presentation layer depends on `NoteUseCase`, and the use cases depend on the `INoteRepository` interface. Room only appears in the data layer.
- **Unidirectional data flow:** the UI sends `NotesEvent`s, the `NotesViewModel` reduces them into an immutable `NotesState`.
- **Ordering as domain logic:** `NoteOrder` / `OrderType` are sealed classes in the domain layer, so sorting rules can be unit-tested without Android.

## 🛠️ Stack

Kotlin · Jetpack Compose · Material 3 · Coroutines + Flow · Room · Dagger Hilt · Navigation Compose

## ▶️ Run

Open in Android Studio and run the `app` configuration (minSdk 24).

## 🗺️ Next steps

- [ ] Add/Edit note screen
- [ ] Unit tests for use cases and `NotesViewModel`
- [ ] Migrate kapt → KSP
