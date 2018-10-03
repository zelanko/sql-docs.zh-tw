---
title: 建立擴充預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ec645ca897bb3760cb5ac866fbc28de5e2f6fcab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711802"
---
# <a name="creating-extended-stored-procedures"></a>建立擴充預存程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序是包含原型的函數：  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 使用前置詞 xp_ 是選擇性的。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中參考時，無論安裝在伺服器上的字碼頁/排序次序為何，擴充預存程序名稱都會區分大小寫。 當您建立 DLL 時：  
  
-   如果需要進入點，撰寫 DllMain 函數。  
  
     此函數是選擇性的；如果您在原始程式碼中沒有提供此函數，編譯器會連結其自己的版本，這個版本只會傳回 TRUE。 如果您提供 DllMain 函數，當執行緒或處理序附加到 DLL 或從 DLL 卸離時，作業系統會呼叫此函數。  
  
-   系統必須匯出從 DLL 外部呼叫的所有函數 (所有擴充預存程序函數)。  
  
     您可以藉由列出其名稱的.def 檔案的 EXPORTS 區段裡匯出函式，或您可以使用 __declspec （dllexport），Microsoft 編譯器延伸模組的原始程式碼中的函式名稱的首碼 (請注意， \__declspec() 開頭為兩個底線)。  
  
 建立擴充預存程序 DLL 時需要這些檔案。  
  
|檔案|描述|  
|----------|-----------------|  
|Srv.h|擴充預存程序 API 標頭檔案|  
|Opends60.lib|Opends60.dll 的匯入程式庫|  
  
 若要建立擴充預存程序 DLL，建立動態連結程式庫類型的專案。 如需有關建立 DLL 的詳細資訊，請參閱開發環境文件集。  
  
 強烈建議您所有擴充預存程序 DLL 都實作並匯出下列函數：  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec (dllexport) 是 Microsoft 專用的編譯器副檔名。 如果您的編譯器不支援此指示詞，您應該在 DEF 檔案的 EXPORTS 區段下匯出這個函數。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]開頭為追蹤旗標-t260 時，或者如果具備系統管理員權限的使用者執行 DBCC TRACEON (260)，而且如果擴充預存程序 DLL 不支援 __getxpversion （），一則警告訊息 (錯誤 8131： 擴充預存程序DLL '%' 並未匯出\__GetXpVersion().) 會列印到錯誤記錄檔。 (請注意， \__GetXpVersion() 開頭為兩個底線。)  
  
 如果擴充預存程序 DLL 匯出 __GetXpVersion()，但是函數所傳回的版本低於伺服器所需要的版本，敘述函數所傳回之版本以及伺服器所需之版本的警告訊息就會列印到錯誤記錄檔中。 如果您收到此訊息時，您要傳回不正確的值從\__GetXpVersion()，或者您正在編譯之舊版的 srv.h 進行編譯。  
  
> [!NOTE]  
>  SetErrorMode 是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 函數，不應該在擴充預存程序中呼叫。  
  
 建議長時間執行的擴充預存程序應該定期呼叫 srv_got_attention，讓該程序可以在連接遭到清除或批次遭到中止時自行結束。  
  
 若要為擴充預存程序 DLL 偵錯，將其複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn 目錄。 若要指定偵錯工作階段的可執行檔，請輸入的路徑和檔案名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可執行檔 (例如，C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\Binn\Sqlservr.exe)。 如需有關 sqlservr 引數的資訊，請參閱[sqlservr 應用程式](../../tools/sqlservr-application.md)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_got_attention&#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
