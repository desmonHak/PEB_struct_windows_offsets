# PEB_struct_windows_offsets

----

offsets de los campos miembros del PEB en windows:

----

```nasm

    ; typedef struct _PEB
    ; {
    ;      BOOLEAN InheritedAddressSpace;     ; 1byte 
    ;                                         ; offset(0x0)
    ;      BOOLEAN ReadImageFileExecOptions;  ; 1byte
    ;                                         ; offset(0x1)
    ;      BOOLEAN BeingDebugged;             ; 1byte 
    ;                                         ; offset(0x2)
    ;      ______________________________________________________
    ;      BOOLEAN SpareBool;
    ;      ------------------------------------------------------
    ;      union {
    ;           UCHAR BitField;
    ;           struct {
    ;               /*  bit fields, follow link  */
    ;           };
    ;       };                              ; 1byte
    ;                                       ; offset(0x3)
    ;       ______________________________________________________
    ;
    ;       ______________________________________________________
    ;       UCHAR Padding0 [4];
    ;      ------------------------------------------------------
    ;      ; ----------- 1 byte ------------------
    ;      ULONG ImageUsesLargePages: 1;                ;1bit
    ;      ULONG IsProtectedProcess: 1;                 ;1bit
    ;      ULONG IsLegacyProcess: 1;                    ;1bit
    ;      ULONG IsImageDynamicallyRelocated: 1;        ;1bit
    ;      ULONG SpareBits: 4;                          ;4bit
    ;      ; -------------------------------------
    ;                                                   ; offset(64bits)(0x4)
    ;       ______________________________________________________
    ;
    ;      HANDLE Mutant; ; offset(64bits)(0x8)
    ;                     ; offset(32bits)(0x4)
    ;
    ;      PVOID ImageBaseAddress; ; 4bytes(32bits), 8bytes(64bits)
    ;                              ; offset(32bits)(0x08)
    ;                              ; offset(64bits)(0x10)
    ;
    ;      PPEB_LDR_DATA Ldr; ; offset(32bits)(0x0c)
    ;                         ; offset(64bits)(0x18)
    ;
    ;      PRTL_USER_PROCESS_PARAMETERS ProcessParameters; ; offset(32bits)(0x10)
    ;                                                      ; offset(64bits)(0x20)
    ;
    ;      PVOID SubSystemData;      ; offset(32bits)(0x14)
    ;                                ; offset(64bits)(0x28)
    ;
    ;      PVOID ProcessHeap;   ; offset(32bits)(0x18)
    ;                           ; offset(64bits)(0x30)
    ;
    ;      ______________________________________________________
    ;      PVOID FastPebLock;
    ;      ------------------------------------------------------
    ;      RTL_CRITICAL_SECTION *FastPebLock;
    ;                   ; offset(32bits)(0x1C)
    ;                   ; offset(64bits)(0x38)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      PVOID AtlThunkSListPtr;
    ;      ------------------------------------------------------
    ;      PVOID SparePtr1;
    ;      ------------------------------------------------------
    ;      PVOID FastPebLockRoutine;
    ;                   ; offset(32bits)(0x20)
    ;                   ; offset(64bits)(0x40)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      PVOID IFEOKey;
    ;      ------------------------------------------------------
    ;      PVOID SparePtr2;
    ;      ------------------------------------------------------
    ;      PVOID IFEOKey;
    ;                   ; offset(32bits)(0x24)
    ;                   ; offset(64bits)(0x48)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      union {
    ;          ULONG CrossProcessFlags;
    ;          struct {
    ;              /*  bit fields, follow link  */
    ;          };
    ;      };
    ;      ------------------------------------------------------
    ;      ULONG EnvironmentUpdateCount;
    ;                   ; offset(32bits)(0x28)
    ;                   ; offset(64bits)(0x50)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      UCHAR Padding1 [4];
    ;      ------------------------------------------------------
    ;      ULONG ProcessInJob: 1;           ; 1bit
    ;      ULONG ProcessInitializing: 1;    ; 1bit
    ;      ULONG ReservedBits0: 30;         ; 30bits
    ;                   ; offset(64bits)(0x54)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      union
    ;      {
    ;           PVOID KernelCallbackTable;
    ;           PVOID UserSharedInfoPtr;
    ;      };
    ;      ------------------------------------------------------
    ;      PVOID KernelCallbackTable;
    ;                   ; offset(32bits)(0x2C)
    ;                   ; offset(64bits)(0x58)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      unaccounted 0x10 bytes ; 3.10 only
    ;      ------------------------------------------------------
    ;      unaccounted four bytes ; 3.50 only
    ;                   ; offset(32bits)(0x28 (3.10))
    ;                   ; offset(32bits)(0x2C (3.50))
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      ULONG SystemReserved[1];  ; 5.1 to 1703
    ;                   ; offset(32bits)(0x30)
    ;      ------------------------------------------------------
    ;      ULONG SystemReserved [2]; ; 5.0 only
    ;                   ; offset(64bits)(0x60)
    ;                   ; offset(32bits)(0x30)
    ;      ------------------------------------------------------
    ;      ULONG SystemReserved;     ; 1709 and higher
    ;                   ; offset(32bits)(0x30)
    ;      ______________________________________________________
    ;
    ;      PVOID EventLog;  ; offset(32bits)(0x34 (3.50 to 4.0))
    ;
    ;      ______________________________________________________
    ;      struct {
    ;          ULONG ExecuteOptions : 2;
    ;          ULONG SpareBits : 30;
    ;      }; ; early 5.1; early 5.2
    ;
    ;               ----------------------------
    ;               ULONG SpareUlong; ; late 5.2 to 6.0
    ;               ----------------------------
    ;               ULONG AtlThunkSListPtr32; ; 	late 5.1; 6.1 and higher
    ;                   ; offset(64bits)(0x64)
    ;               ----------------------------
    ;
    ;      ; offset(32bits)(0x34)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________
    ;      PEB_FREE_BLOCK * FreeList; ; 3.10 to early 6.0
    ;      ------------------------------------------------------
    ;      ULONG SparePebPtr0;        ; late 6.0 only
    ;      ------------------------------------------------------
    ;      PVOID ApiSetMap;           ; 6.1 and higher
    ;                   ; offset(32bits)(0x38)
    ;                   ; offset(64bits)(0x68)
    ;      ______________________________________________________
    ;
    ;      ULONG TlsExpansionCounter;   ; offset(32bits)(0x3C)
    ;                                   ; offset(64bits)(0x70)
    ;      UCHAR Padding2 [4];          ; offset(64bits)(0x74(6.3 and higher))
    ;
    ;      PVOID TlsBitmap;   ; offset(32bits)(0x40)
    ;                         ; offset(64bits)(0x78)
    ;      ULONG TlsBitmapBits[2];   ; offset(32bits)(0x44)
    ;                                ; offset(64bits)(0x80)
    ;      PVOID ReadOnlySharedMemoryBase;   ; offset(32bits)(0x4C)
    ;                                        ; offset(64bits)(0x88)
    ;
    ;      ______________________________________________________
    ;      PVOID HotpatchInformation;      ; (6.0 to 6.2)
    ;      ------------------------------------------------------
    ;      PVOID ReadOnlySharedMemoryHeap; ; (3.10 to 5.2)
    ;      ------------------------------------------------------
    ;      PVOID SparePvoid0;              ; (6.3 to 1607)
    ;      ------------------------------------------------------
    ;      PVOID SharedData;               ; (1703 and higher) 
    ;                   ; offset(32bits)(0x50)
    ;                   ; offset(64bits)(0x90)
    ;      ______________________________________________________
    ;
    ;      PVOID *ReadOnlyStaticServerData;   ; offset(32bits)(0x54)
    ;                                         ; offset(64bits)(0x98)
    ;      PVOID AnsiCodePageData;   ; offset(32bits)(0x58)
    ;                                ; offset(64bits)(0xA0)
    ;      PVOID OemCodePageData;    ; offset(32bits)(0x5C)
    ;                                ; offset(64bits)(0xA8)
    ;      PVOID UnicodeCaseTableData;    ; offset(32bits)(0x60)
    ;                                     ; offset(64bits)(0xB0)
    ;      ULONG NumberOfProcessors;    ; offset(64bits)(0xB8) (3.51 and higher)
    ;                                   ; offset(32bits)(0x64)
    ;      ULONG NtGlobalFlag;    ; offset(64bits)(0xBC) (3.51 and higher)
    ;                             ; offset(32bits)(0x68)
    ;      LARGE_INTEGER CriticalSectionTimeout;    ; offset(32bits)(0x68 (3.10 to 3.50);0x70)
    ;                                               ; offset(64bits)(0xC0)
    ;      ULONG_PTR  HeapSegmentReserve;   ; offset(32bits)(0x78) (3.51 and higher)
    ;                                       ; offset(64bits)(0xC8)
    ;      ULONG_PTR  HeapSegmentCommit;    ; offset(32bits)(0x7C) (3.51 and higher)
    ;                                       ; offset(64bits)(0xD0)
    ;      ULONG_PTR  HeapDeCommitTotalFreeThreshold;   ; offset(32bits)(0x80) (3.51 and higher)
    ;                                                   ; offset(64bits)(0xD8)
    ;      ULONG_PTR  HeapDeCommitFreeBlockThreshold;   ; offset(32bits)(0xD8) (3.51 and higher)
    ;                                                   ; offset(64bits)(0xE0)
    ;      ULONG NumberOfHeaps;             ; offset(32bits)(0x88) (3.51 and higher)
    ;                                       ; offset(64bits)(0xE8)
    ;      ULONG MaximumNumberOfHeaps;      ; offset(32bits)(0x8C) (3.51 and higher)
    ;                                       ; offset(64bits)(0xEC)
    ;      PVOID * ProcessHeaps;   ; offset(32bits)(0x90) (3.51 and higher)
    ;                              ; offset(64bits)(0xF0)
    ;      PVOID GdiSharedHandleTable;   ; offset(32bits)(0x94) (3.51 and higher)
    ;                                    ; offset(64bits)(0xF8)
    ;      PVOID ProcessStarterHelper;   ; offset(32bits)(0x98) (4.0 and higher)
    ;                                    ; offset(64bits)(0x0100)
    ;      ULONG GdiDCAttributeList;     ; offset(32bits)(0x9C) (4.0 and higher)
    ;                                    ; offset(64bits)(0x0100)
    ;      UCHAR Padding3 [4];  ; offset(64bits)(0x010C) (6.3 and higher)
    ;
    ;
    ;      ______________________________________________________
    ;      RTL_CRITICAL_SECTION *LoaderLock; (5.2 and higher)
    ;      ------------------------------------------------------
    ;      PVOID LoaderLock; (4.0 to 5.1)
    ;                   ; offset(32bits)(0xA0)
    ;                   ; offset(64bits)(0x0110)
    ;      ______________________________________________________
    ;
    ;      ULONG OSMajorVersion;     ; offset(32bits)(0xa4)(4.0 and higher)
    ;                                ; offset(64bits)(0x0118)
    ;      ULONG OSMinorVersion;     ; offset(32bits)(0xa8)(4.0 and higher)
    ;                                ; offset(64bits)(0x011C)
    ;      WORD OSBuildNumber;       ; offset(32bits)(0xac)(4.0 and higher)
    ;                                ; offset(64bits)(0x0120)
    ;      WORD OSCSDVersion;       ; offset(32bits)(0xAE)(4.0 and higher)
    ;                               ; offset(64bits)(0x0122)
    ;      ULONG OSPlatformId; ; offset(32bits)(0xB0)(4.0 and higher)
    ;                          ; offset(64bits)(0x0124)
    ;      ULONG ImageSubsystem;     ; offset(32bits)(0xB4)(4.0 and higher)
    ;                                ; offset(64bits)(0x0128)
    ;      ULONG ImageSubsystemMajorVersion;     ; offset(32bits)(0xB8)(4.0 and higher)
    ;                                            ; offset(64bits)(0x012C)
    ;      ULONG ImageSubsystemMinorVersion;     ; offset(32bits)(0xBC)(4.0 and higher)
    ;                                            ; offset(64bits)(0x0130)
    ;      UCHAR Padding4 [4]   ; offset(64bits)(0x0134) (6.3 and higher)
    ;
    ;      ______________________________________________________ 
    ;      KAFFINITY ImageProcessAffinityMask; (4.0 to early 6.0)
    ;      ------------------------------------------------------
    ;      KAFFINITY ActiveProcessAffinityMask; (late 6.0 and higher)
    ;                   ; offset(32bits)(0xC0)
    ;                   ; offset(64bits)(0x0138)
    ;      ______________________________________________________
    ;
    ;      ______________________________________________________ 
    ;      ULONG GdiHandleBuffer[0x22];     (4.0 and higher (x86))
    ;      ------------------------------------------------------
    ;      ULONG GdiHandleBuffer [0x3C];    (all (x64))
    ;                   ; offset(32bits)(0xC4)
    ;                   ; offset(64bits)(0x0140)
    ;      ______________________________________________________ 
    ;
    ;      VOID (*PostProcessInitRoutine) (VOID);    (5.0 and higher)
    ;                   ; offset(32bits)(0x014C)
    ;                   ; offset(64bits)(0x0230)
    ;      PVOID TlsExpansionBitmap;    (5.0 and higher)
    ;                   ; offset(32bits)(0x0150)
    ;                   ; offset(64bits)(0x0238)
    ;      ULONG TlsExpansionBitmapBits[0x20];    (5.0 and higher)
    ;                   ; offset(32bits)(0x0154)
    ;                   ; offset(64bits)(0x0240)
    ;      ULONG SessionId;    (5.0 and higher)
    ;                   ; offset(32bits)(0x01D4)
    ;                   ; offset(64bits)(0x02C0)
    ;   
    ;      UCHAR Padding5 [4]; ; (6.3 and higher)  ; offset(64bits)(0x02C4)
    ;
    ;      ULARGE_INTEGER AppCompatFlags;        (5.1 and higher)
    ;                   ; offset(32bits)(0x01D8)
    ;                   ; offset(64bits)(0x02C8)
    ;      ULARGE_INTEGER AppCompatFlagsUser;    (5.1 and higher)
    ;                   ; offset(32bits)(0x01E0)
    ;                   ; offset(64bits)(0x02D0)
    ;      PVOID pShimData;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x01E8)
    ;                   ; offset(64bits)(0x02D8)
    ;
    ;      PVOID AppCompatInfo;     (5.0 and higher)
    ;                   ; offset(32bits)(0x01D8 (5.0);0x01EC)
    ;                   ; offset(64bits)(0x02E0)
    ;
    ;      UNICODE_STRING CSDVersion;     (5.0 and higher)
    ;                   ; offset(32bits)(0x01DC (5.0);0x01F0)
    ;                   ; offset(64bits)(0x02E8)
    ;
    ;      _ACTIVATION_CONTEXT_DATA * ActivationContextData;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x01F8)
    ;                   ; offset(64bits)(0x02F8)
    ;      _ASSEMBLY_STORAGE_MAP * ProcessAssemblyStorageMap;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x01FC)
    ;                   ; offset(64bits)(0x0300)
    ;      _ACTIVATION_CONTEXT_DATA * SystemDefaultActivationContextData;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x0200)
    ;                   ; offset(64bits)(0x0308)
    ;      _ASSEMBLY_STORAGE_MAP * SystemAssemblyStorageMap;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x0204)
    ;                   ; offset(64bits)(0x0310)
    ;      ULONG_PTR MinimumStackCommit;                       (5.1 and higher)
    ;                   ; offset(32bits)(0x0208)
    ;                   ; offset(64bits)(0x0318)
    ;
    ;      ========================================================
    ;      ; Appended for Windows Server 2003
    ;
    ;      ______________________________________________________ 
    ;      _FLS_CALLBACK_INFO * FlsCallback; (5.2 to 1809)
    ;      ------------------------------------------------------
    ;      PVOID SparePointers [4]; (1903 and higher)
    ;                   ; offset(32bits)(0x020C)
    ;                   ; offset(64bits)(0x0320)
    ;      ______________________________________________________ 
    ;
    ;      LIST_ENTRY FlsListHead;                       (5.2 to 1809)
    ;                   ; offset(32bits)(0x0210 (5.2 to 1809))
    ;                   ; offset(64bits)(0x0328)
    ;
    ;      PVOID FlsBitmap;                       (5.2 to 1809)
    ;                   ; offset(32bits)(0x0218 (5.2 to 1809))
    ;                   ; offset(64bits)(0x0338)
    ;
    ;      ______________________________________________________ 
    ;      ULONG FlsBitmapBits[4]; (5.2 to 1809)
    ;      ------------------------------------------------------
    ;      ULONG SpareUlongs [5];   (1903 and higher)
    ;                   ; offset(32bits)(0x021C)
    ;                   ; offset(64bits)(0x0340)
    ;      ______________________________________________________ 
    ;
    ;      ULONG FlsHighIndex;                      (5.2 to 1809)
    ;                   ; offset(32bits)(0x022C (5.2 to 1809))
    ;                   ; offset(64bits)(0x0350)
    ;
    ;      ========================================================
    ;      ; Appended for Windows Vista
    ;      PVOID WerRegistrationData;                     (6.0 and higher)
    ;                   ; offset(32bits)(0x0230)
    ;                   ; offset(64bits)(0x0358)
    ;      PVOID WerShipAssertPtr;                     (6.0 and higher)
    ;                   ; offset(32bits)(0x0234)
    ;                   ; offset(64bits)(0x0360)
    ;
    ;      ========================================================
    ;      ; Appended for Windows 7
    ;      ______________________________________________________ 
    ;      PVOID pContextData; (6.1 only)
    ;      ------------------------------------------------------
    ;      PVOID pUnused;   (6.2 and higher)
    ;                   ; offset(32bits)(0x0238)
    ;                   ; offset(64bits)(0x0368)
    ;      ______________________________________________________ 
    ;
    ;      PVOID pImageHeaderHash; (6.1 and higher)
    ;                   ; offset(32bits)(0x023C)
    ;                   ; offset(64bits)(0x0370)
    ;
    ;      union {
    ;          ULONG TracingFlags;
    ;          struct {
    ;              /*  bit fields, follow link  */
    ;          };
    ;      }; (6.1 and higher)
    ;                   ; offset(32bits)(0x0240)
    ;                   ; offset(64bits)(0x0378)
    ;
    ;
    ;      ========================================================
    ;      ; Appended for Windows 8
    ;
    ;      ULONGLONG CsrServerReadOnlySharedMemoryBase; (6.2 and higher)
    ;                   ; offset(32bits)(0x0248)
    ;                   ; offset(64bits)(0x0380)
    ;
    ;
    ;      ========================================================
    ;      ; Appended for Windows 10
    ;
    ;      ULONG TppWorkerpListLock;    (1511 and higher)
    ;                   ; offset(32bits)(0x0250)
    ;                   ; offset(64bits)(0x0388	)
    ;
    ;      LIST_ENTRY TppWorkerpList;   (1511 and higher)
    ;                   ; offset(32bits)(0x0254	)
    ;                   ; offset(64bits)(0x0390	)
    ;
    ;      PVOID WaitOnAddressHashTable [0x80];     (1511 and higher)
    ;                   ; offset(32bits)(0x025C	)
    ;                   ; offset(64bits)(0x03A0	)
    ;
    ;      PVOID TelemetryCoverageHeader;   (1709 and higher)
    ;                   ; offset(32bits)(0x045C	)
    ;                   ; offset(64bits)(0x07A0	)
    ;
    ;      ULONG CloudFileFlags;    (1709 and higher)
    ;                   ; offset(32bits)(0x0460	)
    ;                   ; offset(64bits)(0x07A8	)
    ;
    ;      ULONG CloudFileDiagFlags;    (1803 and higher)
    ;                   ; offset(32bits)(0x0464	)
    ;                   ; offset(64bits)(0x07AC	)
    ;
    ;      CHAR PlaceholderCompatibiltyMode;    (1803 and higher)
    ;                   ; offset(32bits)(0x0468	)
    ;                   ; offset(64bits)(0x07B0	)
    ;
    ;      CHAR PlaceholderCompatibilityModeReserved [7]; (1803 and higher)
    ;                   ; offset(32bits)(0x0469	)
    ;                   ; offset(64bits)(0x07B1	)
    ;
    ;      LEAP_SECOND_DATA *LeapSecondData; (1809 and higher)
    ;                   ; offset(32bits)(0x0470	)
    ;                   ; offset(64bits)(0x07B8	)
    ;
    ;      union {
    ;          ULONG LeapSecondFlags;
    ;          struct {
    ;              ULONG SixtySecondEnabled : 1;
    ;              ULONG Reserved : 31;
    ;          };
    ;      }; (1809 and higher)
    ;                   ; offset(32bits)(0x0474	)
    ;                   ; offset(64bits)(0x07C0	)
    ;
    ;      ULONG NtGlobalFlag2;
    ;                   ; offset(32bits)(0x0478	)
    ;                   ; offset(64bits)(0x07C4	)
    ;
    ;
    ; } PEB, *PPEB;

```


-----
