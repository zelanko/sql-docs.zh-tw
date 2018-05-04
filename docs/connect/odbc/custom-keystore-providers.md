---
title: 自訂金鑰存放區提供者 |Microsoft 文件
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
caps.latest.revision: 1
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: ea1e976d4759951c229aa528c18436dbddcfa889
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="custom-keystore-providers"></a>自訂金鑰存放區提供者
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概觀

SQL Server 2016 的資料行加密功能需要加密資料行加密金鑰 (ECEKs) 儲存在伺服器上是由用戶端擷取，並再解密資料行加密金鑰 (Cek) 才能存取加密資料行中儲存的資料。 ECEKs 加密的資料行主要金鑰 (Cmk)，，CMK 的安全性很重要的資料行加密的安全性。 因此，CMK 應該儲存在安全的位置。資料行加密金鑰存放區提供者的目的是提供介面，讓 ODBC 驅動程式，以安全地存取這些儲存 Cmk。 針對具有自己的安全存放裝置的使用者，自訂金鑰存放區提供者介面提供的架構實作安全的 ODBC 驅動程式，然後可以用來執行 CEK 加密和解密的 CMK 存放區的存取權。

包含每個金鑰存放區提供者，並管理一個或多個 Cmk，由金鑰路徑的字串格式的識別提供者定義。 這項目，以及加密演算法，也是提供者，所定義的字串可用來執行的 CEK 加密及解密 ECEK。 演算法，以及 ECEK 和提供者，名稱會儲存在資料庫的加密中繼資料。請參閱[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)和[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)如需詳細資訊。 因此，兩個金鑰管理的基本作業如下：

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

其中`CEKeystoreProvider_name`用來識別特定資料行加密金鑰存放區提供者 (CEKeystoreProvider)，而且其他引數會由 CEKeystoreProvider 來加密/解密 CEK (E)。 機碼路徑與名稱會提供 CMK 中繼資料中，當 CEK 中繼資料所提供的演算法和 ECEK 值。 多個金鑰存放區提供者可能會和預設的內建提供者一起出現。 時執行的作業需要 CEK，驅動程式會使用依名稱，尋找適當的金鑰存放區提供者的 CMK 中繼資料，並執行其解密作業，因為它可以表示為：

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

若要這樣做才能實作作業，例如 CMK 建立和輪替; 雖然驅動程式不需要加密 Cek，可能需要金鑰管理工具這需要執行的反向作業：

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider 介面

本文件詳細說明 CEKeyStoreProvider 介面。 金鑰存放區提供者會實作這個介面可供 Microsoft ODBC Driver for SQL Server。 CEKeyStoreProvider 實作者可以使用本指南來開發自訂金鑰存放區提供者可以使用驅動程式。

金鑰存放區提供者程式庫 （「 提供者程式庫 」） 是可由 ODBC 驅動程式載入動態連結程式庫，而且包含一或多個金鑰存放區提供者。 符號`CEKeystoreProvider`必須由提供者程式庫匯出，而且之 null 終端陣列的指標位址`CEKeystoreProvider`結構，其中每個金鑰存放區提供者程式庫內。

A`CEKeystoreProvider`結構會定義單一金鑰存放區提供者的進入點：

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|欄位名稱|Description|
|:--|:--|
|`Name`|金鑰存放區提供者的名稱。 它不得為先前載入的驅動程式，或存在於此媒體櫃任何其他金鑰存放區提供者相同。 以 null 終止、 寬-字元 * 字串。|
|`Init`|初始化函式。 如果不需要的初始化函式，此欄位可能是 null。|
|`Read`|提供者讀取函式。 可能是 null，如果不需要。|
|`Write`|提供者寫入函式。 需要如果讀取不是 null。 可能是 null，如果不需要。|
|`DecryptCEK`|ECEK 解密函式。 此函式的金鑰存放區提供者存在的原因，並不得為 null。|
|`EncryptCEK`|CEK 加密函式。 驅動程式不會呼叫這個函式，但它可允許以程式設計方式存取 ECEK 建立金鑰管理工具。 可能是 null，如果不需要。|
|`Free`|終止函式。 可能是 null，如果不需要。|

免費版，除了所有此介面中的函式有參數，對**ctx**和**onError**。 前者識別在其中函式呼叫，而後者用來報告錯誤的內容。 請參閱[內容](#context-association)和[錯誤處理](#error-handling)下方如需詳細資訊。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
定義提供者的初始化函式的替代名稱。 驅動程式會呼叫此函式一次之後，提供者已載入，但在第一個要求，以便執行解密 ECEK 或 Read()/Write() 需要的時間。 使用這個函數來執行任何需要的初始化。 

|引數|Description|
|:--|:--|
|`ctx`|[輸入]作業內容。|
|`onError`|[輸入]錯誤報告函式。|
|`Return Value`|傳回非零，表示作業成功，或為零表示失敗。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

定義提供者通訊函式的替代名稱。 應用程式要求讀取 （先前的寫入-至） 提供者使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性，允許應用程式從提供者讀取任意資料的資料時，驅動程式會呼叫此函式。 請參閱[與金鑰存放區提供者通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)如需詳細資訊。

|引數|Description|
|:--|:--|
|`ctx`|[輸入]作業內容。|
|`onError`|[輸入]錯誤報告函式。|
|`data`|[輸出]在其中提供者會將資料讀取應用程式所寫入的緩衝區指標。 這會對應至 CEKEYSTOREDATA 結構的資料欄位。|
|`len`|[InOut]指標長度值。在輸入時，這是資料緩衝區的最大長度，並提供者應該寫入多個 * len 位元組。 傳回時，提供者應該更新 * len 實際寫入的位元組數。|
|`Return Value`|傳回非零，表示作業成功，或為零表示失敗。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
定義提供者通訊函式的替代名稱。 應用程式要求將資料寫入使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性，允許應用程式寫入提供者中的任意資料提供者時，驅動程式會呼叫此函式。 請參閱[與金鑰存放區提供者通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)如需詳細資訊。

|引數|Description|
|:--|:--|
|`ctx`|[輸入]作業內容。|
|`onError`|[輸入]錯誤報告函式。|
|`data`|[輸入]包含要讀取的提供者的資料緩衝區的指標。 這會對應至 CEKEYSTOREDATA 結構的資料欄位。 提供者必須從這個緩衝區讀取多超過 len 位元組。|
|`len`|[輸入]資料中可用的位元組數目。 這會對應到 dataSize CEKEYSTOREDATA 結構欄位。|
|`Return Value`|傳回非零，表示作業成功，或為零表示失敗。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
提供者定義 ECEK 解密函式預留位置名稱。 驅動程式會呼叫此函式來解密 ECEK 加密的 CMK CEK 到與此提供者相關聯。

|引數|Description|
|:--|:--|
|`ctx`|[輸入]作業內容。|
|`onError`|[輸入]錯誤報告函式。|
|`keyPath`|[輸入]值[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) CMK 給定 ECEK 所參考的中繼資料屬性。 以 null 結束寬-字元 * 字串。 這是識別 CMK，此提供者處理。|
|`alg`|[輸入]值[演算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)給定 ECEK 的中繼資料屬性。 以 null 結束寬-字元 * 字串。 這被為了識別用來加密給定的 ECEK 的加密演算法。|
|`ecek`|[輸入]要解密 ECEK 指標。|
|`ecekLen`|[輸入]ECEK 的長度。|
|`cekOut`|[輸出]提供者應該解密 ECEK 配置記憶體，並寫入其位址 cekOut 所指向的指標。 您必須能夠釋放此記憶體使用的區塊[LocalFree](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) 或釋放 (Linux/Mac) 函式。 如果沒有記憶體配置，因為發生錯誤或其他方式，提供者應該將 * cekOut 至 null 指標。|
|`cekLen`|[輸出]提供者應該寫入 cekLen 所指向的位址已寫入解密 ECEK 長度 * * cekOut。|
|`Return Value`|傳回非零，表示作業成功，或為零表示失敗。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
定義提供者的 CEK 加密函數的替代名稱。 驅動程式未呼叫此函式不會公開其功能，透過 ODBC 介面，但它可允許以程式設計方式存取 ECEK 建立金鑰管理工具。

|引數|Description|
|:--|:--|
|`ctx`|[輸入]作業內容。|
|`onError`|[輸入]錯誤報告函式。|
|`keyPath`|[輸入]值[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) CMK 給定 ECEK 所參考的中繼資料屬性。 以 null 結束寬-字元 * 字串。 這是識別 CMK，此提供者處理。|
|`alg`|[輸入]值[演算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)給定 ECEK 的中繼資料屬性。 以 null 結束寬-字元 * 字串。 這被為了識別用來加密給定的 ECEK 的加密演算法。|
|`cek`|[輸入]要加密 CEK 的指標。|
|`cekLen`|[輸入]CEK 的長度。|
|`ecekOut`|[輸出]提供者應該加密 CEK 配置記憶體，並寫入其位址 ecekOut 所指向的指標。 您必須能夠釋放此記憶體使用的區塊[LocalFree](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) 或釋放 (Linux/Mac) 函式。 如果沒有記憶體配置，因為發生錯誤或其他方式，提供者應該將 * ecekOut 至 null 指標。|
|`ecekLen`|[輸出]提供者應該寫入 ecekLen 所指向的位址已寫入加密 CEK 長度 * * ecekOut。|
|`Return Value`|傳回非零，表示作業成功，或為零表示失敗。|

```
void (*Free)();
```
提供者定義終止函式的替代名稱。 驅動程式可能會呼叫此函式的處理序正常終止時。

> [!NOTE]
> *寬字元字串都是因為 SQL Server 如何儲存它們的 2 位元組字元 (utf-16)。*


### <a name="error-handling"></a>錯誤處理

在提供者的處理期間，可能會發生錯誤，因為提供的機制是以允許它更特定的詳細資料，則為 true 的成功/失敗比在回到驅動程式報告錯誤。 許多功能都有一組參數， **ctx**和**onError**，這會針對此目的，除了成功/失敗傳回值一起使用。

**Ctx**參數會識別提供者作業發生的內容。

**OnError**參數指向的錯誤報告的函式，使用下列原型：

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|引數|Description|
|:--|:--|
|`ctx`|[輸入]要在報告錯誤的內容。|
|`msg`|[輸入]要報告的錯誤訊息。 以 null 結束的寬字元字串。 若要允許參數化的資訊必須存在，這個字串可能包含插入格式化序列形式接受[FormatMessage](https://msdn.microsoft.com/library/windows/desktop/ms679351(v=vs.85).aspx)函式。 可能由這個參數指定擴充的功能，如下所述。|
|...|[輸入]其他的 variadic 參數，以符合訊息，視需要的格式規範。|

若要報告發生錯誤時，提供者呼叫 onError 提供內容參數傳入提供者函式的驅動程式和選擇性的額外參數的錯誤訊息中格式化。 提供者可能會呼叫此函式數次發佈多個連續內一個提供者函式引動過程的錯誤訊息。 例如：

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg`參數通常是寬字元字串，但其他延伸模組都會提供：

使用其中一種特殊的預先定義值 IDS_MSG 巨集，與現有的一般錯誤訊息和驅動程式中的 localised 形式可能過高。 例如，如果提供者無法配置記憶體，`IDS_S1_001`可以使用 「 記憶體配置失敗 」 訊息：

`onError(ctx, IDS_MSG(IDS_S1_001));`

錯誤網頁驅動程式，提供者函式必須傳回失敗。 張貼的錯誤這 ODBC 作業的內容中執行時，可透過標準的 ODBC 診斷機制的連接或陳述式控制代碼上進行存取 (`SQLError`， `SQLGetDiagRec`，和`SQLGetDiagField`)。


### <a name="context-association"></a>內容關聯

`CEKEYSTORECONTEXT`結構中，除了提供內容錯誤回呼的資料，也可用來決定執行提供者作業的 ODBC 內容。 這可讓提供者，例如關聯到這些內容中，每個資料來實作每個連線設定。 基於此目的，此結構包含 3 不透明的指標，相對於環境、 連接和陳述式內容：

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```
|欄位|Description|
|:--|:--|
|`envCtx`|環境內容中。|
|`dbcCtx`|連接內容。|
|`stmtCtx`|陳述式的內容。|

這些內容的每一個都是不透明值，而不同於對應的 ODBC 控制代碼，可用來當做唯一識別項控制代碼： 如果處理*X*內容值與相關聯*Y*，然後沒有任何其他環境、 連線或陳述式控制代碼在相同時間同時存在*X*的內容值將會*Y*，以及任何其他內容的值會與相關聯處理*X*。如果提供者作業完成缺少的特定控制代碼的內容，（例如 SQLSetConnectAttr 呼叫載入並設定提供者，這在沒有任何陳述式控制代碼） 對應的結構中的內容值為 null。


## <a name="example"></a>範例

### <a name="keystore-provider"></a>金鑰存放區提供者

下列程式碼是最小金鑰存放區提供者實作的範例。

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>ODBC 應用程式

下列程式碼會示範應用程式會使用上述的金鑰存放區提供者。 當執行它，請確認提供者程式庫與應用程式二進位檔相同的目錄中且的連接字串指定 （或指定包含 DSN）`ColumnEncryption=Enabled`設定。

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>另請參閱

[使用 ODBC 驅動程式搭配使用一律加密](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
