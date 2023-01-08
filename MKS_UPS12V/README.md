# MKS UPS12V

## Firmware (Marlin)

[MyCR10-S Branch on github](https://github.com/pierre-quelin/Marlin)

Configuration_adv.h

      #define POWER_LOSS_RECOVERY
      #if ENABLED(POWER_LOSS_RECOVERY)
        #define PLR_ENABLED_DEFAULT    true // Power Loss Recovery enabled by default. (Set with 'M413 Sn' & M500)
        #define BACKUP_POWER_SUPPLY         // Backup power / UPS to move the steppers on power loss
        #define POWER_LOSS_ZRAISE         2 // (mm) Z axis raise on resume (on power loss with UPS)
        #define POWER_LOSS_PIN          PB1 // Pin to detect power loss. Set to -1 to disable default pin on boards without module.
        #define POWER_LOSS_STATE       HIGH // State of pin indicating power loss
        //#define POWER_LOSS_PULLUP         // Set pullup / pulldown as appropriate for your sensor
        #define POWER_LOSS_PULLDOWN
        #define POWER_LOSS_PURGE_LEN   20   // (mm) Length of filament to purge on resume
        #define POWER_LOSS_RETRACT_LEN 10   // (mm) Length of filament to retract on fail. Requires backup power.
    
        // Without a POWER_LOSS_PIN the following option helps reduce wear on the SD card,
        // especially with "vase mode" printing. Set too high and vases cannot be continued.
        #define POWER_LOSS_MIN_Z_CHANGE 0.05 // (mm) Minimum Z change before saving power-loss data
    
        // Enable if Z homing is needed for proper recovery. 99.9% of the time this should be disabled!
        //#define POWER_LOSS_RECOVER_ZHOME
        #if ENABLED(POWER_LOSS_RECOVER_ZHOME)
          //#define POWER_LOSS_ZHOME_POS { 0, 0 } // Safe XY position to home Z while avoiding objects on the bed
        #endif
      #endif

## MKS-Robin-E3D pinout

[MKS-Robin-E3D-V1.0](https://github.com/pierre-quelin/cr10s/blob/master/MKS_UPS12V/MKS-Robin-E3D-V1.0.jpg)

## Official Makerbase site

[MKS-UPS12V](https://github.com/makerbase-mks/MKS-Power-Control/tree/master/MKS%20UPS12V-24V)
