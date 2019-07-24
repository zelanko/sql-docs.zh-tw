---
title: 自訂金鑰存放區提供者 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006489"
---
# <a name="custom-keystore-providers"></a>自訂金鑰儲存區提供者
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>概觀

SQL Server 2016 的資料行加密功能, 必須由用戶端抓取儲存在伺服器上的加密資料行加密金鑰 (ECEKs), 然後再解密為數據行加密金鑰 (Cek), 才能存取加密資料行中所儲存的資料。 ECEKs 是由資料行主要金鑰 (Cmk) 加密, 而 CMK 的安全性對於資料行加密的安全性很重要。 因此, CMK 應該儲存在安全的位置;資料行加密金鑰存放區提供者的目的是要提供介面, 讓 ODBC 驅動程式能夠存取這些安全儲存的 Cmk。 針對具有自己安全存放裝置的使用者, 自訂金鑰儲存區提供者介面提供了一個架構, 可讓您針對 ODBC 驅動程式的 CMK 安全儲存體進行存取, 然後用來執行 CEK 加密和解密。

每個金鑰存放區提供者都包含並管理一個或多個 Cmk, 這些是由提供者所定義之格式的字串所識別的索引鍵路徑。 這連同加密演算法 (也是由提供者所定義的字串), 都可用來執行 CEK 的加密和解密 ECEK。 演算法 (連同 ECEK 和提供者的名稱) 會儲存在資料庫的加密中繼資料中;如需詳細資訊, 請參閱[建立資料行主要金鑰](../../t-sql/statements/create-column-master-key-transact-sql.md)和[建立資料行加密金鑰](../../t-sql/statements/create-column-encryption-key-transact-sql.md)。 因此, 金鑰管理的兩個基本作業如下:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

`CEKeystoreProvider_name`用來識別特定資料行加密金鑰存放區提供者 (CEKeystoreProvider), 而 CEKeystoreProvider 會使用其他引數來加密/解密 (E) CEK。 名稱和 keypath 是由 CMK 中繼資料所提供, 而演算法和 ECEK 值則是由 CEK 中繼資料提供。 多個金鑰存放區提供者可能會與預設的內建提供者一起出現。 在執行需要 CEK 的作業時, 驅動程式會使用 CMK 中繼資料來依名稱尋找適當的金鑰存放區提供者, 並執行其解密作業, 其可表示為:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

雖然驅動程式不需要加密 Cek, 但金鑰管理工具可能需要這麼做, 才能執行 CMK 建立和輪替等作業;這需要執行反向操作:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>CEKeyStoreProvider 介面

本檔詳細說明 CEKeyStoreProvider 介面。 執行此介面的金鑰存放區提供者可供 Microsoft ODBC Driver for SQL Server 使用。 CEKeyStoreProvider 實施者可以使用此指南來開發驅動程式可用的自訂金鑰儲存區提供者。

金鑰存放區提供者程式庫 (以下稱為「提供者程式庫」) 是可由 ODBC 驅動程式載入的動態連結程式庫, 其中包含一或多個金鑰儲存區提供者。 符號`CEKeystoreProvider`必須由提供者程式庫匯出, 而且是結構之以`CEKeystoreProvider` null 結束之指標陣列的位址, 在程式庫中的每個金鑰儲存區提供者各一個。

`CEKeystoreProvider`結構會定義單一金鑰存放區提供者的進入點:

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
|`Name`|金鑰存放區提供者的名稱。 它不能與驅動程式先前載入的任何其他金鑰存放區提供者相同, 也不得存在於此程式庫中。 以 Null 結尾的寬字元*字串。|
|`Init`|初始化函數。 如果不需要初始化函數, 此欄位可能是 null。|
|`Read`|提供者讀取功能。 如果不需要, 可能會是 null。|
|`Write`|提供者寫入函式。 如果讀取不是 null, 則為必要。 如果不需要, 可能會是 null。|
|`DecryptCEK`|ECEK 解密功能。 此函式是存在金鑰儲存區提供者的原因, 而且不得為 null。|
|`EncryptCEK`|CEK 加密功能。 驅動程式不會呼叫此函式, 但會提供它來允許以程式設計方式存取金鑰管理工具所建立的 ECEK。 如果不需要, 可能會是 null。|
|`Free`|終止函式。 如果不需要, 可能會是 null。|

除了 Free 以外, 此介面中的函式都有一對參數**ctx**和**onError**。 前者會識別呼叫函式的內容, 而後者則是用來報告錯誤。 如需詳細資訊, 請參閱下方的[內容](#context-association)和[錯誤處理](#error-handling)。

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
提供者定義之初始化函數的預留位置名稱。 驅動程式會在載入提供者之後, 但在第一次需要它來執行 ECEK 解密或讀取 ()/Write () 要求之前, 呼叫此函式一次。 使用此函式可執行所需的任何初始化工作。 

|引數|Description|
|:--|:--|
|`ctx`|源作業內容。|
|`onError`|源錯誤-報告函數。|
|`Return Value`|傳回非零表示成功, 或零表示失敗。|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

提供者定義之通訊函數的預留位置名稱。 當應用程式要求使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性從 (先前寫入的) 提供者讀取資料時, 驅動程式會呼叫這個函式, 讓應用程式可以從提供者讀取任意資料。 如需詳細資訊, 請參閱[與金鑰存放區提供者通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|引數|Description|
|:--|:--|
|`ctx`|源作業內容。|
|`onError`|源錯誤-報告函數。|
|`data`|輸出緩衝區的指標, 提供者會在其中寫入要由應用程式讀取的資料。 這會對應至 CEKEYSTOREDATA 結構的資料欄位。|
|`len`|InOut長度值的指標;輸入時, 這是資料緩衝區的最大長度, 而且提供者不能寫入超過 * len 個位元組。 傳回時, 提供者應該以實際寫入的位元組數目來更新 * len。|
|`Return Value`|傳回非零表示成功, 或零表示失敗。|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
提供者定義之通訊函數的預留位置名稱。 當應用程式要求使用 SQL_COPT_SS_CEKEYSTOREDATA 連接屬性將資料寫入提供者時, 驅動程式會呼叫這個函式, 讓應用程式可以將任意資料寫入提供者。 如需詳細資訊, 請參閱[與金鑰存放區提供者通訊](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers)。

|引數|Description|
|:--|:--|
|`ctx`|源作業內容。|
|`onError`|源錯誤-報告函數。|
|`data`|源緩衝區的指標, 其中包含要讀取之提供者的資料。 這會對應至 CEKEYSTOREDATA 結構的資料欄位。 提供者不能從這個緩衝區讀取超過 len 個位元組。|
|`len`|源資料中可用的位元組數目。 這會對應至 CEKEYSTOREDATA 結構的 dataSize 欄位。|
|`Return Value`|傳回非零表示成功, 或零表示失敗。|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
提供者定義之 ECEK 解密函數的預留位置名稱。 驅動程式會呼叫這個函式, 將與此提供者相關聯的 CMK 所加密的 ECEK 解密成 CEK。

|引數|Description|
|:--|:--|
|`ctx`|源作業內容。|
|`onError`|源錯誤-報告函數。|
|`keyPath`|源給定 ECEK 所參考之 CMK 的[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md)中繼資料屬性值。 以 Null 結尾的寬字元*字串。 這是為了識別此提供者所處理的 CMK。|
|`alg`|源給定 ECEK 的[演算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)中繼資料屬性值。 以 Null 結尾的寬字元*字串。 這是用來識別用來加密指定 ECEK 的加密演算法。|
|`ecek`|源要解密之 ECEK 的指標。|
|`ecekLen`|源ECEK 的長度。|
|`cekOut`|輸出提供者應該為解密的 ECEK 配置記憶體, 並將其位址寫入 cekOut 所指向的指標。 您必須能夠使用[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 Free (Linux/Mac) 功能釋放此記憶體區塊。 如果因為發生錯誤而未配置記憶體, 則提供者必須將 * cekOut 設定為 null 指標。|
|`cekLen`|輸出提供者必須 cekLen 已寫入 * * cekOut 的解密 ECEK 長度, 以寫入所指向的位址。|
|`Return Value`|傳回非零表示成功, 或零表示失敗。|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
提供者定義的 CEK 加密功能的預留位置名稱。 驅動程式不會呼叫此函式, 也不會透過 ODBC 介面公開其功能, 但會提供此功能, 以允許以程式設計方式存取金鑰管理工具所建立的 ECEK。

|引數|Description|
|:--|:--|
|`ctx`|源作業內容。|
|`onError`|源錯誤-報告函數。|
|`keyPath`|源給定 ECEK 所參考之 CMK 的[KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md)中繼資料屬性值。 以 Null 結尾的寬字元*字串。 這是為了識別此提供者所處理的 CMK。|
|`alg`|源給定 ECEK 的[演算法](../../t-sql/statements/create-column-encryption-key-transact-sql.md)中繼資料屬性值。 以 Null 結尾的寬字元*字串。 這是用來識別用來加密指定 ECEK 的加密演算法。|
|`cek`|源要加密之 CEK 的指標。|
|`cekLen`|源CEK 的長度。|
|`ecekOut`|輸出提供者應該為加密的 CEK 配置記憶體, 並將其位址寫入 ecekOut 所指向的指標。 您必須能夠使用[LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 或 Free (Linux/Mac) 功能釋放此記憶體區塊。 如果因為發生錯誤而未配置記憶體, 則提供者必須將 * ecekOut 設定為 null 指標。|
|`ecekLen`|輸出提供者必須 ecekLen 已寫入 * * ecekOut 的加密 CEK 長度, 以寫入所指向的位址。|
|`Return Value`|傳回非零表示成功, 或零表示失敗。|

```
void (*Free)();
```
提供者定義之終止函式的預留位置名稱。 驅動程式可能會在進程正常終止時呼叫此函式。

> [!NOTE]
> *寬字元字串是2位元組字元 (UTF-16), 因為 SQL Server 儲存它們的方式。*


### <a name="error-handling"></a>錯誤處理

當提供者的處理過程中發生錯誤時, 系統會提供一項機制, 讓它向驅動程式報告錯誤, 而不是布林值成功/失敗的詳細資料。 許多函式都有一對參數 ( **ctx**和**onError**), 除了成功/失敗傳回值之外, 也會用於此用途。

**Ctx**參數會識別提供者作業所在的內容。

**OnError**參數會指向錯誤報表函式, 並具有下列原型:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|引數|Description|
|:--|:--|
|`ctx`|源報告錯誤的內容。|
|`msg`|源要報告的錯誤訊息。 以 Null 結尾的寬字元字串。 若要允許參數化資訊出現, 此字串可能包含[FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage)函數接受之表單的插入格式序列。 此參數可指定擴充功能, 如下所述。|
|...|源適用的其他 variadic 參數, 以符合 msg 中的格式規範。|

若要在發生錯誤時報告, 提供者會呼叫 onError, 並提供驅動程式所傳遞至提供者函式的內容參數, 以及要在其中格式化的選擇性其他參數的錯誤訊息。 提供者可以多次呼叫此函式, 以在一個提供者函式呼叫中連續張貼多個錯誤訊息。 例如：

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg`參數通常是寬字元字串, 但有其他延伸模組可供使用:

藉由搭配使用其中一個特殊的預先定義值與 IDS_MSG 宏, 就可以利用驅動程式中已存在的一般錯誤訊息, 並以經過當地語系化的形式呈現。 例如, 如果提供者無法配置記憶體, 則`IDS_S1_001`可以使用「記憶體配置失敗」訊息:

`onError(ctx, IDS_MSG(IDS_S1_001));`

對於要由驅動程式副檔名被的錯誤, 提供者函式必須傳回失敗。 在 ODBC 作業的內容中執行此作業時, 會透過標準 ODBC 診斷機制 (`SQLError`、 `SQLGetDiagRec`和`SQLGetDiagField`), 在連接或語句控制碼上存取張貼的錯誤。


### <a name="context-association"></a>內容關聯

除了提供錯誤回呼的內容之外, 還可以使用結構來決定執行提供者作業所在的ODBC內容。`CEKEYSTORECONTEXT` 這可讓提供者將資料與上述每個內容產生關聯, 例如, 用來執行每個連線設定。 基於此目的, 結構包含3個對應至環境、連接和語句內容的不透明指標:

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
|`envCtx`|環境內容。|
|`dbcCtx`|連接內容。|
|`stmtCtx`|語句內容。|

這些內容都是不透明的值, 而不是對應的 ODBC 控制碼, 可以當做控制碼的唯一識別碼: 如果控制碼*X*與內容值*Y*相關聯, 則沒有其他環境、連接或語句會同時存在於與*x*相同的時間, 其內容值為*Y*, 而且沒有其他內容值會與 handle *X*相關聯。如果完成的提供者作業缺少特定的控制碼內容 (例如, SQLSetConnectAttr 呼叫來載入和設定提供者, 其中沒有語句控制碼), 則結構中的對應內容值為 null。


## <a name="example"></a>範例

### <a name="keystore-provider"></a>金鑰儲存區提供者

下列程式碼是最小金鑰存放區提供者實作為的範例。

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

下列程式碼是使用上述金鑰存放區提供者的示範應用程式。 執行時, 請確定提供者程式庫位於與應用程式二進位檔相同的目錄中, 而且連接字串指定 (或指定包含的 DSN) `ColumnEncryption=Enabled`設定。

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
