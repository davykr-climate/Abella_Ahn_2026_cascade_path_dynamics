# Revealing Risk Through Cascade Path Dynamics in Compounding Dry Hazards

**Supplementary computational workflow** for the study:  
*Revealing Risk Through Cascade Path Dynamics in Compounding Dry Hazards*  
Abella, D. & Ahn, KH (2026)

---

## Purpose

This repository provides **methodological transparency** for our analysis of compound dry hazards (heatwaves, droughts, and fire) and their cascade pathways. Code is presented as **pseudocode** for:

1. Data pre-processing of the data used from ERA5  
2. Thresholds for hazard detection
3. Heatwave, drought, and fire detection
4. Compound dry hazards identification
5. Cascade path classification

---

## Workflow Overview

```mermaid
flowchart TD
    A[ERA5 Raw Data<br>1980–2023] --> B[Daily Hazard Variables]
    B --> B1[Tmax °C<br>from t2m]
    B --> B2[Precip mm<br>from tp]
    B --> B3[FWI<br>from fwinx]
    
    B1 --> C1[95th Percentile<br>31-day window]
    B2 --> C2[SPI360<br>Gamma fit]
    B3 --> C3[95th Percentile<br>31-day window]
    
    C1 --> D1[Heatwave<br>≥3 days ≥ P95]
    C2 --> D2[Drought<br>SPI < -1.5]
    C3 --> D3[Fire Hazard<br>FWI ≥ P95]
    
    D1 & D2 & D3 --> E[Compound Hazard Map<br>Binary encoding:<br>0=none, 1=H, 2=D, 3=F,<br>4=HD, 5=HF, 6=DF, 7=HDF]
    
    E --> F[Cascade Path Classification<br>• Single→Compound<br>• Compound→Compound<br>• Recurrent Events<br>• Recovery Paths]
