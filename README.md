# Decoder-Layout-Design-and-challenges

Design of 7nm Decoder and Challenges faced while making

## Layout Screenshot of Complete 4x16 Decoder
<img width="1853" height="990" alt="Screenshot from 2026-11-19 10-31-10" src="https://github.com/user-attachments/assets/240c3888-4831-4e88-8c99-9522b1d6760d" />


To make Layout of 4x16 Decoder, first i had made a single decoder whose schematic is attached

<img width="533" height="151" alt="image" src="https://github.com/user-attachments/assets/69cd387f-5620-42e0-8a27-0ef253d8867e" />

A) Decoder-1 Layout Challenges

    ► Decoder-1 to be made in 2-bitcell pitch as it has 3-input nand gate and bitcell is in 2 poly pitch
    ► WL metal track runs across the cell, enabling access from both ends in butter-fly memory.
    ►  Clock (DCLK) to be least loaded, should run right above its nand gate and nand gate connection on boundary to be shared to reduce DCLK capacitance.
    ► PreA, PreB, and PreC of 3-input nand gate are programming signals hance it gates to be made to be access for programmation.
    ► Boundaries should have supplies or signals shared for adjacent cells like DCLK and PreB, PreC signals as both boundaries are shared by itself as in the bitcell

## Layout Screenshot of single Decoder
<img width="455" height="565" alt="image" src="https://github.com/user-attachments/assets/a3aaf3df-2017-4bb7-851b-481de499826a" />

B) Made Layout of two Decoder, whose schematic i have attached
<img width="1326" height="193" alt="image" src="https://github.com/user-attachments/assets/c2b5f764-7217-4711-be6d-13c9af64fa37" />

Its layout challenges are

    ► Instantiate Decoder-1 in R0
    ► Then another Decoder-1, instantiate it in MX
    ► Put PreA<1:3>, VDD, PreC<0:7>, VSS, PreB<0:7>, VDD, PreA<0:2> between the cells
    ► Program PreA<0>, PreB<0>, PreC<0>, PreA<1> at this cell level
    ► Supply shielding within sets PreA–PreB, and PreB–PreC and PreC–PreA eliminate intra pre-lines coupling.
    ► Within set PreA or PreB or PreC coupling is allowed to gaining area and load of pre-line programmation.

C) Made Layout of 4 Decoder, called as chunk of 4, by calling instantiation of Decoder-2 (R0+MX) twice in R0+MY orientation, Its schematic i have attached
<img width="1376" height="339" alt="image" src="https://github.com/user-attachments/assets/cc2fcfd9-6bc2-4d86-b334-fa6aac6a7777" />

Layout challenges kept in mind

    ► Instantiate Decoder-2 in R0
    ► Then another Decoder-2, instantiate it in MY
    ► Remove programmation of PreA<0:1> lines from Decoder-2
    ► Program PreA<0:3> at this cell level
    ► Lavel DCLK and supplies and WL<0:3> according to programmation.
    ► Lavel PreA<0:3> PreB<0> and PreC<0> for LVS

## Layout Screenshot of chunk of 4 Decoder
<img width="1857" height="1042" alt="image" src="https://github.com/user-attachments/assets/bde0d683-6c97-4e51-94d0-2221da5a0a25" />

D) Finally made 4x16 Decoder Layout by calling instantiation of chunk of 4 decoder, instances being called 16 times in R0 orientation

    ► programmation of predec lines PreA<0:3> for a chunk of 4 Decoder and its repeat from PreA<0:3> for all 16 Chunks
    ► Programmation of predec lines PreB, PreB0 common for 1st chunk, PreB1 common for 2nd chunk....similarly PreB7 common for 8th Chunk of Decoder
    ► At 9th chunk to 16th chunk PreB<0:7> will again repeat similarly
    ► programmation of predec lines PreC<0:7>, for eight chunks PreC0 will be common for all 0-31 Decoder then for another eight chunks PreC1 will be common for 32-63 Decoders
    ► DCLK signal coming from control would be common for all 64 Decoders
    ► Sets of PreA<0:3>, PreB<0:7>, PreC<0:7> predec lines will be sheileded with power rails to avoid coupling effect

## Layout screenshot of 4x16 Decoder has been attached on TOP
