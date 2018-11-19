## Externe Library hinzufühgen
    yarn add amazing-time-picker
    yarn add momentjs
    yarn add moment-timezone

Komponenen Modul in *shared.module.ts* hinzufügen


    import { AmazingTimePickerModule } from 'amazing-time-picker';
    mports: [
        ....
        AmazingTimePickerModule
    ],