# MK11 VR Hasher
Code to hash MK11's data in order to properly send requests to the api endpoints. VR Hash check is introduced on 15th of September 2020.

# Usage

 1. You need to use the provided Cheat Table in order to obtain the 4 IV values from the game. Should Enable the script while the game is loading but before you "Press Start".
 2. Get the IV Values and the string you want to hash.
 
 Usage Command is
 

    vr-hasher IV1 IV2 IV3 IV4 String_To_Hash

## Notes
I'm retrieving the 4 IVs after they're being calculated from 1 initial IV. This is because the 4 IVs are in the registers at a specific point during execution, which is less prone to change during updates than trying to retrieve from the stack. (`mov $data, RAX ` is less prone to update than `mov RAX, [ESP+20]`). The point of obtaining the code uses AOB scan over a function that _theoritically_ doesn't change, so it should work across new updates as well. Finally, the address of _this_ pointer that stores the IV struct is **0x143176620** as of Sep-15-2020. IV Struct is at **addr+0x1390**, which translates to **0x1431779B0**. The initial (seed?) value is at **IV Struct + 0x20** which is used to create the other 3 values, and the remaining the 3 IV values are at **RSP+0x70  RSP+0x88, R11**.

Memory Snapshot after IV calculation:

    RAX 8080808080808081
    RBX 1
    RCX Not Needed
    RDX IV
    RBP len(TS_String)
    RSP Not Needed
    RSI CCCCCCCCCCCCCCCD
    RDI 2492492492492493
    R8  FFFFFFFF
    R9  IV
    R10 IV2
    R11 IV
    R12 loop ctr
    R13 TS_STRING DAY_HOUR:MINUTE:SEC_IDslug
    R14 AAAAAAAAAAAAAAAB
    R15 loop ctr
    RSP+70 IV3
    rsp+88 IV4
    rsp+20 IV2
