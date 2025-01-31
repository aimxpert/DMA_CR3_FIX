inside of FixCr3 find where it sasy "[+] Patched DTB\n" and right before it add this:

static ULONG64 pml4[512];
DWORD readsize;
VMMDLL_MemReadEx(this->vHandle, -1, dtb, reinterpret_cast<PBYTE>(pml4), sizeof(pml4), (PDWORD)&readsize, VMMDLL_FLAG_NOCACHE | VMMDLL_FLAG_NOPAGING | VMMDLL_FLAG_ZEROPAD_ON_FAIL | VMMDLL_FLAG_NOPAGING_IO);
VMMDLL_MemReadEx((VMM_HANDLE)-666, 333, (ULONG64)pml4, 0, 0, 0, 0);
VMMDLL_ConfigSet(this->vHandle, VMMDLL_OPT_PROCESS_DTB | current_process.PID, 666);
