
Properties
Impedance at 100Mhz
DC Resistance
Rated DC Current (IDC) + Derating
Impedance vs DC bias (current)

- **Impedance at a stated frequency (usually @ 100 MHz)**
    
    - Typical choices for supply filtering: **~100–600 Ω @ 100 MHz**.
        
    - Higher isn’t always better (can resonate with caps).
        
- **DC resistance (DCR)**
    
    - Lower is better so you don’t drop DC voltage.
        
    - For VREF/analog rails, aim **as low as practical** (often **< 0.2 Ω**, many are much lower).
        
- **Rated DC current (IDC) + derating**
    
    - Must exceed your steady current **with margin**.
        
    - For VREF it’s usually tiny (µA–mA), but if the bead feeds other analog loads, size accordingly.
        
- **Impedance vs DC bias (current)**
    
    - Beads lose impedance when DC current flows.
        
    - For VREF (low current) this is usually a non-issue, but it matters on bigger rails.
        
- **Frequency/impedance curve (and material type)**
    
    - Check the graph: you want attenuation where your noise lives (often **1–300 MHz** for digital edges).
        
    - Choose a bead whose impedance peaks in the noisy band.
        
- **Package size & parasitics (0603/0402/0805, etc.)**
    
    - Smaller packages have lower inductance but lower current rating; pick what matches your layout/current.
        
- **SRF / resonance behavior**
    
    - Bead + caps can create peaking. If you see ringing issues, sometimes a _moderate_ bead (not huge Ω) is better.
        
- **Temperature rating / automotive grade** (if needed)