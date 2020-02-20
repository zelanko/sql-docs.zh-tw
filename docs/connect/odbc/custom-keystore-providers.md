---
title: 自訂金鑰儲存區提供者 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68006489"
---
# <a name="custom-keystore-providers"></a>自訂金鑰儲存區提供者
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概觀

SQL Server 2016 的資料行加密功能必須由用戶端擷取儲存在伺服器上的加密資料行加密金鑰 (ECEK)，然後再解密為資料行加密金鑰 (CEK)，才能存取加密資料行中所儲存的資料。 ECEK 是由資料行主要金鑰 (CMK) 加密，而 CMK 的安全性對於資料行加密的安全性很重要。 因此，CMK 應該儲存在安全的位置；資料行加密金鑰儲存區提供者的目的是要提供介面，讓 ODBC 驅動程式能夠存取這些安全儲存的 CMK。 針對擁有自己的安全存放裝置的使用者，自訂金鑰儲存區提供者介面會提供一個架構，可讓您針對 ODBC 驅動程式的 CMK 安全存放裝置進行存取，然後用來執行 CEK 加密和解密。

每個金鑰儲存區提供者都包含並管理一或多個透過金鑰路徑所識別的 CMK，也就是由提供者所定義之格式的字串。 這連同加密演算法 (也是由提供者所定義的字串) 都可用來執行 CEK 的加密和 ECEK 的解密。 演算法 (連同 ECEK 和提供者的名稱) 會儲存在資料庫的加密中繼資料中；如需詳細資訊，請參閱[建立資料行主要金鑰](../../t-sql/statements/create-column-master-key-transact-sql.md)和[建立資料行加密金鑰](../../t-sql/statements/create-column-encryption-key-transact-sql.md)。 因此，金鑰管理的兩個基本作業如下：

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

其中 `CEKeystoreProvider_name` 用來識別特定的資料行加密金鑰儲存區提供者 (CEKeystoreProvider)，而 CEKeystoreProvider 會使用其他引數來加密/解密 (E)CEK。 名稱和 keypath 是由 CMK 中繼資料所提供，而演算法和 ECEK 值則是由 CEK 中繼資料提供。 多個金鑰儲存區提供者可能會與預設的內建提供者同時存在。 在執行需要 CEK 的作業時，驅動程式會使用 CMK 中繼資料，依名稱尋找適當的金鑰儲存區提供者，並執行其解密作業，其可表示為：

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

雖然驅動程式不需要加密 CEK，但是金鑰管理工具可能需要這麼做，才能實作 CMK 建立和變換等作業；這需要執行反向操作：

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider 介面

此文件詳細描述 CEKeyStoreProvider 介面。 實作此介面的金鑰儲存區提供者可供 Microsoft ODBC Driver for SQL Server 使用。 CEKeyStoreProvider 實施者可以使用本指南開發驅動程式可用的自訂金鑰儲存區提供者。

金鑰儲存區提供者程式庫 (以下稱為「提供者程式庫」) 是一個可由 ODBC 驅動程式載入的動態連結程式庫，其中包含一或多個金鑰儲存區提供者。 `CEKeystoreProvider` 符號必須由提供者程式庫匯出，而且必須是指向 `CEKeystoreProvider` 結構並以 Null 結束之指標陣列的位址，也就是供程式庫中每個金鑰儲存區提供者使用的位址。

`CEKeystoreProvider` 結構會定義單一金鑰儲存區提供者的進入點：

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

|欄位名稱|描述|
|:--|:--|
|`Name`|金鑰儲存區提供者的名稱。 其不得與驅動程式先前載入的其他任何金鑰儲存區提供者相同，也不得存在於此程式庫中。 以 Null 結尾的寬字元*字串。|
|`Init`|初始化函式。 如果不需要初始化函式，此欄位可能是 Null。|
|`Read`|提供者 read 函式。 如果不需要，可能是 Null。|
|`Write`|提供者 write 函式。 如果 Read 不是 Null，則為必要。 如果不需要，可能是 Null。|
|`DecryptCEK`|ECEK 解密函式。 此函式是金鑰儲存區提供者存在的原因，因此不得為 Null。|
|`EncryptCEK`|CEK 加密函式。 驅動程式不會呼叫此函式，但會提供此函式來允許以程式設計方式存取金鑰管理工具所建立的 ECEK。 如果不需要，可能是 Null。|
|`Free`|終止函式。 如果不需要，可能是 Null。|

除了 Free 以外，此介面中的函式都有一對參數，**ctx** 和 **onError**。 前者會識別呼叫函式的內容，而後者則是用來報告錯誤。 如需詳細資訊，請參閱下面的[內容](#context-association)和[錯誤處理](#error-handling)。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
提供者定義之初始化函式的預留位置名稱。 驅動程式會在載入提供者之後，但在第一次驅動程式需要此函式來執行 ECEK 解密或 Read()/Write() 要求之前，呼叫此函式一次。 使用此函式可執行所需的任何初始化工作。 

|引數|描述|
|:--|:--|
|`ctx`|[輸入] 作業內容。|
|`onError`|[輸入] 錯誤報告函式。|
|`Return Value`|傳回非零表示成功，傳回零表示失敗。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

提供者定義之通訊函式的預留位置名稱。 當應用程式要求使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性從 (先前寫入的) 提供者讀取資料時，驅動程式會呼叫這個函式，進而讓應用程式可以讀取來自提供者的任意資料。 如需詳細資訊，請參閱[與金鑰儲存區提供者進行通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|引數|描述|
|:--|:--|
|`ctx`|[Input] 作業內容。|
|`onError`|[Input] 錯誤報告函式。|
|`data`|[Output] 緩衝區的指標，提供者會在其中寫入要由應用程式讀取的資料。 這會對應至 CEKEYSTOREDATA 結構的 data 欄位。|
|`len`|[InOut] 長度值的指標；輸入時，這是資料緩衝區的最大長度，而且提供者不得在其中寫入超過 *len 個位元組。 傳回時，提供者應該以實際寫入的位元組數目來更新 *len。|
|`Return Value`|傳回非零表示成功，傳回零表示失敗。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
提供者定義之通訊函式的預留位置名稱。 當應用程式要求使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性將資料寫入至提供者時，驅動程式會呼叫這個函式，進而讓應用程式可以將任意資料寫入至提供者。 如需詳細資訊，請參閱[與金鑰儲存區提供者進行通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|引數|描述|
|:--|:--|
|`ctx`|[Input] 作業內容。|
|`onError`|[Input] 錯誤報告函式。|
|`data`|[Input] 緩衝區的指標，其中包含要讀取之提供者的資料。 這會對應至 CEKEYSTOREDATA 結構的 data 欄位。 提供者不得從這個緩衝區讀取超過 len 個位元組。|
|`len`|[Input] 資料中可用的位元組數目。 這會對應至 CEKEYSTOREDATA 結構的 dataSize 欄位。|
|`Return Value`|傳回非零表示成功，傳回零表示失敗。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
提供者定義之 ECEK 解密函式的預留位置名稱。 驅動程式會呼叫這個函式，將與此提供者相關聯的 CMK 所加密的 ECEK 解密成 CEK。

|引數|描述|
|:--|:--|
|`ctx`|[Input] 作業內容。|
|`onError`|[Input] 錯誤報告函式。|
|`keyPath`|[Input] 給定 ECEK 所參考 CMK 之 [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) 中繼資料屬性的值。 以 Null 結尾的寬字元*字串。 這是為了識別此提供者所處理的 CMK。|
|`alg`|[Input] 給定 ECEK 之 [ALGORITHM](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 中繼資料屬性的值。 以 Null 結尾的寬字元*字串。 這是用來識別加密給定 ECEK 所使用的加密演算法。|
|`ecek`|[Input] 要解密之 ECEK 的指標。|
|`ecekLen`|[Input] ECEK 的長度。|
|`cekOut`|[Output] 提供者應該為解密的 ECEK 配置記憶體，並將其位址寫入至 cekOut 所指向的指標。 您必須可以使用 [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 free (Linux/Mac) 函式釋放這個記憶體區塊。 如果因為發生錯誤而未配置記憶體，則提供者應該將 *cekOut 設定為 Null 指標。|
|`cekLen`|[Output] 提供者應該將 cekLen 已寫入至 **cekOut 的解密 ECEK 長度，寫入至 cekLen 所指向的位址。|
|`Return Value`|傳回非零表示成功，傳回零表示失敗。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
提供者定義之 CEK 加密函式的預留位置名稱。 驅動程式不會呼叫此函式，也不會透過 ODBC 介面公開其功能，但會提供此函式來允許以程式設計方式存取金鑰管理工具所建立的 ECEK。

|引數|描述|
|:--|:--|
|`ctx`|[Input] 作業內容。|
|`onError`|[Input] 錯誤報告函式。|
|`keyPath`|[Input] 給定 ECEK 所參考 CMK 之 [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) 中繼資料屬性的值。 以 Null 結尾的寬字元*字串。 這是為了識別此提供者所處理的 CMK。|
|`alg`|[Input] 給定 ECEK 之 [ALGORITHM](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 中繼資料屬性的值。 以 Null 結尾的寬字元*字串。 這是用來識別加密給定 ECEK 所使用的加密演算法。|
|`cek`|[Input] 要加密之 CEK 的指標。|
|`cekLen`|[Input] CEK 的長度。|
|`ecekOut`|[Output] 提供者應該為加密的 CEK 配置記憶體，並將其位址寫入至 ecekOut 所指向的指標。 您必須可以使用 [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 free (Linux/Mac) 函式釋放這個記憶體區塊。 如果因為發生錯誤而未配置記憶體，則提供者應該將 *ecekOut 設定為 Null 指標。|
|`ecekLen`|[Output] 提供者應該將 ecekLen 已寫入至 **ecekOut 的加密 CEK 長度，寫入至 ecekLen 所指向的位址。|
|`Return Value`|傳回非零表示成功，傳回零表示失敗。|

```
void (*Free)();
```
提供者定義之終止函式的預留位置名稱。 驅動程式可能會在處理序正常終止時呼叫此函式。

> [!NOTE]
> *寬字元字串因為 SQL Server 將其儲存的方式，而成為 2 個位元組的字元 (UTF-16)。*


### <a name="error-handling"></a>錯誤處理

當提供者的處理過程中發生錯誤時，系統會提供一項機制，讓其向驅動程式更詳細地回報錯誤，而不是回報布林值成功/失敗。 許多函式都有 **ctx** 和 **onError** 這一對參數，除了成功/失敗傳回值之外，也會用於此目的。

**ctx** 參數會識別提供者作業所在的內容。

**onError** 參數會指向錯誤報告函式，並具有下列原型：

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|引數|描述|
|:--|:--|
|`ctx`|[Input] 報告錯誤的內容。|
|`msg`|[Input] 要報告的錯誤訊息。 以 Null 結尾的寬字元字串。 為允許參數化資訊出現，此字串可包含 [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) 函式所接受之表單的插入格式序列。 此參數可指定擴充功能，如下所述。|
|...|[Input] 其他 variadic 參數，可符合 msg 中的格式規範 (如果適用的話)。|

為了在發生錯誤時報告，提供者會呼叫 onError，以提供驅動程式傳遞至提供者函式的內容參數，以及要在其中格式化的其他選用參數的錯誤訊息。 提供者可以多次呼叫此函式，以便在一個提供者函式叫用中連續張貼多個錯誤訊息。 例如：

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg` 參數通常是寬字元字串，但有其他擴充功能可供使用：

透過搭配 IDS_MSG 巨集使用其中一個預先定義的特殊值，就可以利用驅動程式中已存在的一般錯誤訊息，並以當地語系化的形式呈現。 例如，如果提供者無法配置記憶體，則可以使用 `IDS_S1_001`「記憶體配置失敗」訊息：

`onError(ctx, IDS_MSG(IDS_S1_001));`

對於驅動程式所辨識的錯誤，提供者函式必須傳回失敗。 當此作業在 ODBC 作業的內容中執行時，會透過標準 ODBC 診斷機制 (`SQLError`、`SQLGetDiagRec` 和 `SQLGetDiagField`)，在連接或陳述式控制代碼上存取張貼的錯誤。


### <a name="context-association"></a>內容關聯

除了提供錯誤回呼的內容之外，`CEKEYSTORECONTEXT` 結構也可以用來決定執行提供者作業所在的 ODBC 內容。 這可讓提供者將資料與上述每個內容產生關聯，例如，用來實作每個連線設定。 基於此目的，結構包含 3 個對應至環境、連接和陳述式內容的不透明指標：

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|欄位|描述|
|:--|:--|
|`envCtx`|環境內容。|
|`dbcCtx`|連接內容。|
|`stmtCtx`|陳述式內容。|

這些內容都是不透明的值 (而且與對應的 ODBC 控制代碼不同)，可用來當作控制代碼的唯一識別碼使用：如果控制代碼 *X* 與內容值 *Y* 相關聯，則與 *X* 同時存在的其他任何環境、連接或陳述式控制代碼都不會有 *Y* 的內容值，而且不會有其他任何內容值與控制代碼 *X* 相關聯。如果正在完成的提供者作業缺少特定的控制代碼內容 (例如，用於載入和設定提供者的 SQLSetConnectAttr 呼叫，其中沒有陳述式控制代碼)，則結構中的對應內容值為 Null。


## <a name="example"></a>範例

### <a name="keystore-provider"></a>金鑰儲存區提供者

下列程式碼是最小金鑰儲存區提供者實作的一個範例。

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

下列程式碼是使用上述金鑰儲存區提供者的示範應用程式。 執行時，請確定提供者程式庫位於與應用程式二進位檔相同的目錄中，而且連接字串會指定 `ColumnEncryption=Enabled` 設定或指定包含該設定的 DSN。

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

[搭配使用 Always Encrypted 與 JDBC 驅動程式](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
