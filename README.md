# Archivos de entrada DFT — AlF₃ sobre e intercalado en grafito

Material complementario de la tesis doctoral

**Sorción molecular en grafito pirolítico altamente orientado**
Heidy Stefany Betancourt Infante — Instituto de Física del Litoral (IFIS-Litoral, CONICET–UNL), Santa Fe, Argentina.
Director: Dr. Fernando J. Bonetto. Codirector: Dr. Gustavo D. Ruano.

Los cálculos se describen en los Capítulos 4 y 5 de la tesis y en:

> H. S. Betancourt-Infante, G. D. Ruano, F. J. Bonetto, S. J. Rodríguez-Sotelo,
> *Cooperative adsorption and hindered diffusion induced by AlF₃ intercalation in graphite*,
> Applied Surface Science **755**, 168736 (2027). https://doi.org/10.1016/j.apsusc.2026.168736

## Contenido

Archivos de entrada representativos de OpenMX 3.9, uno por tipo de cálculo.

| Carpeta | Archivo | Sistema | Tipo de cálculo |
|---|---|---|---|
| `01_referencias` | `grafito_bulk_7x6x1.dat` | Grafito Bernal *bulk*, 168 C | Relajación atómica (RF), k 6×6×6 |
| | `slab_3capas_7x6x1.dat` | *Slab* de 3 láminas, 252 C | Relajación (RF), k 6×6×1 |
| | `AlF3_aislado.dat` | AlF₃ aislado en la misma celda | Referencia molecular |
| | `dimero_aislado.dat` | Dímero (AlF₃)₂ aislado en la misma celda | Referencia del dímero |
| `02_adsorcion_pristino` | `P1_monomero.dat` | 1 AlF₃ adsorbido sobre grafito prístino | Relajación (RF) |
| | `P_1dimero.dat` | 1 dímero adsorbido sobre grafito prístino | Relajación (RF) |
| `03_intercalacion_blister` | `I1_intercalado.dat` | 1 AlF₃ intercalado (I-1, *blister*) | Relajación (RF) |
| | `B4_dos_dimeros.dat` | 1 AlF₃ intercalado + 2 dímeros superficiales (B4) | Relajación (RF) |
| `04_NEB` | `NEB_pristino_camino_P1.dat` | Camino P1 sobre grafito prístino | NEB, 4 imágenes |
| | `NEB_blister_camino_P3.dat` | Camino P3 sobre superficie con *blister* | NEB, 4 imágenes |
| `05_DOS` | `P1_DOS.dat` | P1 en la geometría relajada | DOS/PDOS, malla 20×20×1 |

Los archivos de relajación y NEB contienen la configuración **de partida** del cálculo correspondiente. El archivo de DOS utiliza la geometría ya relajada.

## Parámetros comunes

- OpenMX 3.9; GGA-PBE + DFT-D3(BJ) (`version.dftD 3`, `DFTD3.damp bj`); sin polarización de espín.
- Pseudopotenciales y bases PAO de la base de datos OpenMX 2019: `Al7.0-s2p2d1 Al_PBE19`, `C6.0-s2p2d1 C_PBE19`, `F6.0-s2p2d1 F_PBE19`.
- `scf.energycutoff` 180 Ry (malla de integración en espacio real; no es un corte de ondas planas).
- Temperatura electrónica 300 K; mezcla RMM-DIIS.
- Supercelda 7×6×1 de la celda hexagonal del grafito: |a₁| = 17.289 Å, |a₂| = 14.819 Å, γ = 120°, altura de celda c = 25 Å (bulk: c = 6.79 Å).
- Todos los átomos libres durante la relajación (`MD.Fixed.XYZ` = 0 0 0).

| Parámetro | Adsorción / intercalación | NEB |
|---|---|---|
| `scf.Kgrid` | 6 6 1 | 4 4 1 |
| `scf.criterion` (Ha) | 1.0e-7 | 1.0e-6 |
| `MD.Opt.criterion` (Ha/bohr) | 4.0e-4 | 4.0e-4 |
| Mezcla inicial / mín. / máx. | 0.010 / 0.001 / 0.002 | 0.05 / 0.003 / 0.1 |
| Historial RMM-DIIS | 7 | 15 |
| `MD.NEB.Number.Images` | — | 4 |
| `MD.NEB.Spring.Const` (Ha/bohr²) | — | 0.1 |

## Uso

Reemplazar `DATA.PATH` por la ruta local a `DFT_DATA19` de OpenMX 3.9 y ejecutar, por ejemplo:

```bash
mpirun -np 32 openmx P1_monomero.dat > P1_monomero.out
```

## Licencia

Los archivos se distribuyen bajo la licencia Creative Commons Attribution 4.0 International (CC BY 4.0). Si los utiliza, cite la tesis o el artículo indicado arriba.
