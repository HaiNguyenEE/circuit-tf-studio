# ⚡ eerfLab — Circuit ⇄ Transfer Function Studio

### The free, offline-first Electrical Engineering & RF lab in a single file — from schematic to H(s), Bode, root locus, state-space, SPICE-grade transient physics, and back to a suggested circuit topology.

**🌐 Live app: [eerflab.com](https://eerflab.com)** · runs 100 % in your browser · no install · no account · works offline

**Phòng thí nghiệm Điện – Điện tử – RF miễn phí, chạy hoàn toàn offline trong trình duyệt: từ sơ đồ mạch → hàm truyền H(s) → Bode / quỹ đạo nghiệm / không gian trạng thái → mô phỏng vật lý thật → và gợi ý ngược lại topology mạch.**

![The complete Arduino UNO Q — all 24 schematic sheets on one canvas, with the neon beacons and the 🔦 finder bar naming the two parts you actually need](v2.79/01-unoq-complete-board-with-finder.png)

**How complex can it get, and can you still find anything?** The **complete Arduino UNO Q** — all **24 schematic sheets** transcribed onto **one canvas**, ≈3 800 parts, every chip pin carrying the PDF's own name — and the app **points at its own entry points**: the programmable MCU and the power input glow, and a 🔦 finder bar names them in words so you never hunt. · **Mạch phức tạp đến đâu, mà vẫn tìm được?** Toàn bộ 24 trang sơ đồ của Arduino UNO Q trên MỘT canvas, ~3 800 linh kiện — và app **tự chỉ vào chỗ cần**: MCU lập trình được và nguồn vào phát sáng, thanh 🔦 gọi tên chúng bằng chữ.

| | |
|---|---|
| ![Double-click the MCU and an Arduino-style IDE opens inside the app — sketch on the left, live Serial monitor on the right](v2.79/07-arduino-style-IDE-serial-streaming.png) | ![▶ Upload hot-swaps a new sketch while the circuit keeps running — the simulation never stops](v2.79/09-hot-swap-Upload-into-a-RUNNING-sim.png) |

---

## 🆕 What's new — v2.79 line

### 🧠 The MCU is programmable, and the IDE is *in* the app
Double-click the MCU on any sheet and an **Arduino-style IDE opens right there**. Write `setup()` / `loop()` with `pinMode` · `digitalWrite` · `digitalRead` · `analogRead` · `analogWrite` · `delay` · `Serial` — and:

- the sketch runs on **simulation time**, not wall-clock (`delay()` yields, so the solver stays in charge);
- `analogWrite()` is a **real 490 Hz PWM** the oscilloscope in the app can actually see — not a DC average;
- `Serial.print` streams to a **live monitor** beside your code;
- **▶ Upload hot-swaps the code while the circuit is still running.** No stop, no reset, no reload — you edit, upload, and watch the waveform change.
- A sketch that doesn't compile is **refused, and the running simulation keeps running.**

Two real part families, both with **per-pin FUNCTION labels printed on the symbol** (`PB5 · D13 · SCK · LED`) — because a pin number alone teaches nothing:

| Part | What it is | Honest behaviour |
|---|---|---|
| **eerfLab-M1** | Friendly 3.3 V teaching MCU, self-powered `3V3` pin, PWM on every D pin | Branded as *ours* — an honest fiction, never sold as a chip we don't model |
| **ATmega328P** | The **Arduino UNO's real chip** | 5 V logic; **you** must power `VCC`/`AVCC`; below the **2.7 V brown-out** the sketch holds in reset; PWM only on **D3/5/6/9/10/11** like a real UNO; `RESET` pin is live; ≈25 Ω drive; 40 mA/pin absolute max is warned |

*VN — Nhấp đúp vào MCU: một IDE kiểu Arduino mở ngay trong app. Sketch chạy theo thời gian mô phỏng, `analogWrite` là PWM 490 Hz thật nhìn thấy trên scope, Serial in ra màn hình bên cạnh, và **▶ Upload thay code khi mạch đang chạy**. Hai họ linh kiện: eerfLab-M1 (3.3 V, dễ dùng) và ATmega328P (chip UNO thật — phải cấp 5 V, có brown-out, đúng 6 chân PWM). Chức năng từng chân ghi thẳng trên ký hiệu.*

| | |
|---|---|
| ![Pick the MCU family in the part editor — eerfLab-M1 or ATmega328P — with the pin documentation right there](v2.79/06-mcu-part-editor-family-and-pin-doc.png) | ![ATmega328P symbol with every pin labelled by its function, not just its number](v2.79/10-ATmega328P-every-pin-labelled.png) |
| ![A new sketch typed into the in-app IDE, before upload](v2.79/08-IDE-new-sketch-typed-before-upload.png) | ![The IDE refuses a sketch that won't compile — and the running simulation keeps running](v2.79/09b-IDE-refuses-a-bad-sketch.png) |

### 🔦 Key-part beacons — a crowded sheet must point at its own entry points
On a board with thousands of parts, "where do I program this?" and "where does power come in?" are the only two questions that matter first. So the app answers them without being asked: the programmable MCU and the power source carry a **neon halo sized in screen pixels** (unmistakable even at the fit-view of the whole UNO Q) plus a caption naming the **action** — *PROGRAM HERE — double-click → IDE* / *POWER IN*. A **🔦 finder bar** lists every key part in words; click a chip and the view **flies straight there**. The bar tracks the page scroll, so it is still on screen when you scroll into the board. A sheet author can flag any part with their own bilingual caption and colour, saved with the sheet.

*VN — Trên bảng mạch hàng nghìn linh kiện, app tự chỉ: MCU và nguồn vào có quầng neon (đo bằng pixel màn hình nên luôn nhìn rõ) kèm chú thích nói rõ HÀNH ĐỘNG. Thanh 🔦 gọi tên từng phần quan trọng — bấm một chip là bay thẳng tới đó, và thanh này bám theo cuộn trang.*

| | |
|---|---|
| ![Click a finder chip and the view flies straight to the MCU](v2.79/02-finder-chip-flies-to-the-MCU.png) | ![The same finder walks you to the 12 V input](v2.79/03-finder-chip-flies-to-the-12V-input.png) |
| ![The finder bar tracks the page scroll — still on screen once you are inside the board](v2.79/04-finder-survives-the-page-scroll.png) | ![An example sketch running on the MCU, driving the circuit around it](v2.79/05-mcu-sketch-example-running.png) |

### 🧮 H(s) → circuit: a cascade is now the **product of what it draws**
A synthesised cascade used to be checked stage by stage — and stage-by-stage "✓ exact" proves nothing about the chain. Now **every section is normalised to unity at its own reference band** before any gain is placed on it, gain is only assigned to a stage that **provably carries it** (the built circuit is read back and measured, because a unity-gain Sallen-Key throws `K` away entirely), and whatever no stage can carry is **declared as a leftover instead of vanishing**.

The visible result: a 3rd-order Butterworth stage that asked for **`R1 = 403 µΩ`** — not a resistor, less than the wire you'd solder it with — now reads **`R1 = 15.9 kΩ`**, and the drawn chain multiplies back out to `H(s)` exactly (it was off by **×3.9 × 10⁷** at 3rd order, ×1.5 × 10¹⁵ at 5th). Polarity is derived from the count of inverting stage templates rather than from a magnitude, so a 180° flip no longer demands a pointless unity-gain op-amp. Pinned permanently by **112 gates** that multiply every preset's *drawn* stages back against the target.

*VN — Cascade bây giờ đúng bằng TÍCH của những gì nó vẽ ra: mỗi tầng được chuẩn hoá về 1 tại dải tham chiếu của chính nó, độ lợi chỉ đặt lên tầng thật sự gánh được (đo ngược lại từ mạch đã dựng), phần còn dư được KHAI BÁO chứ không biến mất. `R1 = 403 µΩ` → `R1 = 15.9 kΩ`.*

![Type any H(s) and the studio designs the circuit — cascade op-amp stages with real, orderable E-series values](v2.79/16-Hs-to-real-opamp-synthesis.png)

### ⚡ And the rest of the r14 arc
- **The UNO Q power section actually powers up** — a real 12 V on the barrel jack through modelled **LMR51440 + two TPS62A02A** bucks lands **4.989 / 3.742 / 3.318 V**, the **47 ms power-good delay** gates the USB host handover, and the green power LED draws 3.88 mA.
- **Indexed geometry (E58)** replaced the all-pairs scans: netlist **978 → 73 ms**, lint **3696 → 151 ms** — pan and zoom stay interactive with the whole board mounted.
- **Save/load keeps your sketches**, block pins and declared clocks (E59); double-click works **during** a live run (E57).

---

## 🧭 A complete solution — Schematic → Simulation → Analysis → Suggested Topology

Most tools give you one link of the chain. **eerfLab gives you the whole loop, in both directions:**

| Step | What you get | Công cụ |
|---|---|---|
| **1 · Schematic** | Drag-and-drop schematic editor: sources, passives, diodes/zeners/LEDs, BJT/MOSFET/JFET, transformers, machines, pots/trimmers, relays, fuses, speakers, **programmable MCUs** — plus a library of **93 exact, datasheet-verified ICs** picked by real MPN | Vẽ mạch kéo-thả, linh kiện thật theo mã |
| **2 · Simulation** | One click ▶ — DC operating point, AC → H(s), and a **real time-domain transient engine**: exponential Ebers-Moll BJTs (SPICE `pnjlim` convergence), switch-level power MOSFETs, coupled-inductor transformers, dq-model electric machines, I²t & power-rating "boom" physics, honest refusals when an op point is non-physical | Mô phỏng ⏱ vật lý thật, linh kiện quá tải nổ như đời thực |
| **3 · Analysis** | Exact **H(s)** (MNA nodal analysis + minimal rational fit), factored poles/zeros, Bode with GM/PM markers, step, Nyquist + encirclement criterion, **root locus**, closed-loop step, **state-space ẋ = Ax+Bu (controllable canonical)** with one-click **MATLAB / Python export**, **Monte-Carlo tolerance envelopes and pole clouds**, noise, FFT/THD, PCB trace calculators (IPC-2221/2152) | Phân tích H(s), Bode, Nyquist, quỹ đạo nghiệm, không gian trạng thái, Monte-Carlo, xuất MATLAB/Python |
| **4 · Suggested topology** | Type ANY H(s) and the studio **designs circuits for you**: cascade of first/second-order op-amp stages with concrete E-series R/C values, **KHN state-variable biquads**, lag/lead compensators, and the full **analog-computer integrator chain** — each stage openable back in the Circuit Lab. Unrealisable gain is declared, not hidden; RHP poles are flagged honestly ("needs a stabilizing loop") | Nhập H(s) bất kỳ → app tự đề xuất mạch: cascade op-amp, KHN biquad, chuỗi tích phân analog computer — mở ngược lại vào Circuit Lab |

That loop — **circuit → math → circuit** — is what makes eerfLab a *studio*, not just a simulator.

---

## 📊 By the numbers

- **≈3 800 parts on one canvas** — the complete Arduino UNO Q (ABX00162), all **24 schematic sheets**, every chip pin carrying the PDF's own name, every net a label, the **104-LED matrix**, both 60-pin FFCs, the Arduino headers, 58 DNP, 51 testpoints — and it still pans and zooms
- **93 exact ICs** — datasheet-verified, pin-for-pin, picked by MPN (NE555P, TL431, LM358/LM324/LM741, LM393/LM339, TL08x, CD4000 & 74HC logic families, CD74HC4046A PLL, MAX4374, MC34063, TL494, UC3842, SG3525AN, LMR51440, TPS62A02A, **ATmega328P**, …) with per-part golden tests and refusal diagnostics (floating pins, missing supply, out-of-range VCC)
- **60 + generic component models** — R/L/C/pots, diode family with breakdown & thermal ratings, BJT/MOSFET/JFET, transformers (incl. tapped), machines, relays, fuses, thermistor/LDR/varistor/varactor, speakers, crystals…
- **10 auto-running live examples** — battery protector (MAX4374), 180 V boost (MC34063 + IRF644), SG3525 inverter, 3φ motor, 3φ generator, DC motor, 555 blinker, TL431 regulator, LM358 swing lesson, HC4046 PLL lock — each with a bilingual engineering walk-through in the hint
- **51 headless regression suites / 2 000 + individual checks** run green before every release — solver math, IC golden tests, preset physics, cascade synthesis, UI lint — plus a browser smoke run against the **exact bytes production serves**
- **4 integrated labs** — Circuit Lab → H(s) · H(s) → Circuit · Block Diagrams & Mason's gain formula · RF Lab (Smith chart, S-parameters, matching, stability circles)
- **1 file, 0 servers** — the whole studio ships as a single offline HTML file

---

## 🖼 Gallery

**Real chips, real physics · Chip thật, vật lý thật**

| | |
|---|---|
| ![SG3525 + IRFZ44N H-bridge inverter running live — a 12 V battery becomes 230 V / 50 Hz on the oscilloscope](v2.79/12-SG3525-12V-to-230V-inverter.png) | ![Full 22-transistor Class-AB power amplifier, decoded 1:1 from the original schematic print and solved live](v2.79/13-ClassAB-22-transistor-full-build.png) |
| ![MAX4374F battery protector — a real datasheet part running as a live example](v2.79/14-MAX4374F-battery-protector.png) | ![CD74HC4046A PLL locking onto a 3 kHz reference](v2.79/15-CD74HC4046A-PLL-locking.png) |
| ![The UNO Q power section as a switching close-up, with scope-ready ripple](v2.79/11-UNO-Q-power-section-on-the-scope.png) | ![Boost converter — drag the potentiometer to set the duty cycle and watch the output move](v2.79/20-boost-converter-drag-the-POT.png) |

**Analysis you can trust · Phân tích đáng tin**

| | |
|---|---|
| ![Monte-Carlo tolerance envelope and the resulting pole cloud](v2.79/13b-Monte-Carlo-tolerance-and-pole-cloud.png) | ![Block diagrams solved by Mason's gain formula, cross-checked by an independent node-equation solver](v2.79/17-block-diagrams-Mason-cross-check.png) |
| ![Three-phase induction motor — full stationary-frame dq dynamic model](v2.79/19-three-phase-induction-motor-dq.png) | ![RF Lab — nodal S-parameter solver and Smith chart](v2.79/18-RF-lab-S-parameters-and-Smith.png) |
| ![Bode plot with gain & phase margin markers, computed exactly from the drawn circuit](12-bode-gm-pm.png) | ![Root locus — poles, zeros, asymptotes and closed-loop gain sweep](15-root-locus.png) |
| ![Control view: loop shaping and closed-loop response side by side](16-control-view-closedloop.png) | ![Honest step response — real solver output with settling metrics, never a faked curve](17-step-response-honest.png) |
| ![Load-example menu: auto-running teaching circuits, each with a bilingual engineering walk-through](13-live-examples-menu.png) | ![Exact-part picker — 93 datasheet-verified ICs chosen by real manufacturer part number](14-exact-part-picker.png) |

**More from the bench · Thêm từ bàn làm việc**

| | |
|---|---|
| ![Live Class-AB amplifier in the Circuit Lab](01-circuit-live-amp.png) | ![Diode and zener live physics — breakdown and thermal ratings modelled](02-diode-zener-live.png) |
| ![NE555 blinker running as a live example](08-555-blinker-live.png) | ![Modulation quality — constellation and EVM through AWGN, phase noise and PA compression](06-modulation-evm.png) |

---

## 🎓 Who it's for

- **Students** — see *why* the textbook Bode plot looks that way; drag a slider and watch poles move; write a sketch and watch the PWM on a scope
- **Educators** — every live example is a prepared lecture: real chips, real failure modes, honest limitations
- **Practicing engineers** — quick H(s) sanity checks, compensator sketches, state-space export to MATLAB/Python, PCB trace-width math
- **Hobbyists & makers** — build the inverter or the 555 blinker exactly like the web schematic — except this one has been debugged for you

*No account. No cloud. Your designs stay on your machine.*

---

## 🔑 Keywords / Từ khóa

free online circuit simulator · transfer function calculator · H(s) from circuit · Bode plot online · Nyquist plot · root locus tool · state-space realization · controllable canonical form · MNA nodal analysis · SPICE alternative in browser · Arduino simulator online · ATmega328P simulator · Arduino IDE in browser · MCU PWM simulation · Arduino UNO Q schematic · op-amp filter synthesis · KHN biquad designer · Sallen-Key · lag lead compensator · Monte Carlo tolerance analysis · Mason's gain formula solver · signal flow graph · Smith chart matching · S-parameters · SG3525 inverter simulation · MC34063 boost converter · class AB amplifier design · 555 timer circuit · PLL CD4046 · three-phase induction motor simulation · DC motor transient · power electronics lab · electrical engineering education — mô phỏng mạch điện online miễn phí · hàm truyền · đồ thị Bode · quỹ đạo nghiệm · tổng hợp mạch op-amp · mô phỏng Arduino · mạch nghịch lưu SG3525 · động cơ không đồng bộ 3 pha · phòng thí nghiệm điện tử ảo

---

## 🚀 Try it now

**→ [eerflab.com](https://eerflab.com)** — press **Load example**, pick the 🧩 Arduino UNO Q, follow the 🔦 finder to the MCU, **double-click it**, and upload a sketch into a board that is already running.

*Built with an obsession for honest physics: if the model can't simulate something faithfully, it says so — in English and Vietnamese.*

---

## 📄 Usage & license

**Free to use, but not open source.** The hosted web application is free for personal, educational and professional work. The source code is proprietary and is not published here — copying, redistributing, modifying, reverse-engineering or creating derivative works requires prior written consent. See [`LICENSE`](LICENSE).

*Miễn phí sử dụng, nhưng không phải mã nguồn mở. Mã nguồn không được công bố ở đây; xem [`LICENSE`](LICENSE).*

— **Hai (Steve) Nguyen** · Electrical Engineering, CSULB · [LinkedIn](https://www.linkedin.com/in/hai-nguyen-ee)
