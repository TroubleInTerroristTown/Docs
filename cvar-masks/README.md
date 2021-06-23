# CVar Masks



Masks are used extensively within CS:GO in order to represent different options that can coexist. One of the more common uses within the TTT project itself is to be able to choose multiple roles within a single CVAR.

Consider the following values:

```c
#define TTT_TEAM_UNASSIGNED (1 << 0) // 0001 in binary, 1 in decimal
#define TTT_TEAM_INNOCENT (1 << 1) // 0010 in binary, 2 in decimal
#define TTT_TEAM_TRAITOR (1 << 2) // 0100 in binary, 4 in decimal
#define TTT_TEAM_DETECTIVE (1 << 3) // 1000 in binary,  8 in decimal
```

If one wants to enable a mask for both INNOCENT and DETECTIVE but not for either of the other two teams, one can simply add together the decimal values of those items \(8 + 2 = 10\). In binary, this is represented as `1010`. This format allows us to quickly determine whether a a number has that specified flag enabled using an AND operation, e.g.:

```c
TTT_TEAM_TRAITOR & 10 // false
TTT_TEAM_DETECTIVE & 10 // true
```

Examples for convar values:

* 2 - Innocent
* 4 - Traitor
* 8 - Detective
* 6 \(2 + 4\) - Innocent + Traitor
* 10 \(2 + 8\) - Innocent + Detective
* 12 \(4 + 8\) - Traitor + Detective
* 14 \(2 + 4 + 8\) - Innocent + Traitor + Detective

