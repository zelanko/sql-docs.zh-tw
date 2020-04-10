---
title: 連線 bcp | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0967f40a4f38156babe2f5fd736e57b5567cbdcc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924548"
---
# <a name="connecting-with-bcp"></a>連接 bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[Bcp](https://go.microsoft.com/fwlink/?LinkID=190626) 公用程式可在 Linux 和 macOS 版 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上使用。 此頁面記錄了與 Windows 版本 `bcp` 的差異。
  
- 欄位結束字元是定位字元 ("\t")。  
  
- 行結束字元是新行字元 ("\n")。  
  
- 字元模式是不含擴充字元的 `bcp` 格式檔案和資料檔案的慣用格式。  
  
> [!NOTE]  
> 命令列引數上的反斜線 '\\' 必須加上引號或逸出。 例如，若要將新行字元指定為自訂資料列結束字元，您必須使用下列其中一種機制：  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
以下是將資料表資料列複製到文字檔的 `bcp` 範例命令呼叫：  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>可用的選項
在目前版本中，有下列語法和選項可供使用：  

[_database_ **.** ]_schema_ **.** _table_ **in** _data\_file_ | **out** _data\_file_

- -a *packet_size*  
指定伺服器所收送之每個網路封包的位元組數。  
  
- -b *batch_size*  
指定每一批次匯入資料的資料列數。  
  
- -c  
使用字元資料類型。  
  
- -d *database_name*  
指定要連接的資料庫。  
  
- -d  
使傳遞至 `bcp` -S 選項的值解譯為資料來源名稱 (DSN)。 如需詳細資訊，請參閱[使用 sqlcmd 進行連線](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)中的＜sqlcmd 和 bcp 中的 DSN 支援＞。  
  
- -e *error_file* 指定錯誤檔的完整路徑，該錯誤檔用來儲存 `bcp` 公用程式無法從檔案傳送至資料庫的任何資料列。  
  
- -E  
將匯入之資料檔案中的識別值用於識別欄位。  
  
- -f *format_file*  
指定格式檔的完整路徑。  
  
- -F *first_row*  
指定要從資料表匯出或從資料檔案匯入之第一個資料列的號碼。  
  
- -k  
指定空白資料行在作業過程中應保持 Null 值，而非保有插入之資料行的任何預設值。  
  
- -l  
指定登入逾時。 -l 選項會指定在您嘗試連線到伺服器時，登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 逾時之前的秒數。 預設登入逾時為 15 秒。 登入逾時必須是介於 0 與 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`bcp` 就會產生錯誤訊息。 值為 0 會指定無限逾時。
  
- -L *last_row*  
指定要從資料表匯出或從資料檔案匯入的最後一個資料列的號碼。  
  
- -m *max_errors*  
指定 `bcp` 作業取消前，可以出現的語法錯誤數上限。  
  
- -n  
使用資料的原生 (資料庫) 資料類型來執行大量複製作業。  
  
- -P *password*  
指定登入識別碼的密碼。  
  
- -Q  
在 `bcp` 公用程式與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之間的連接中，執行 SET QUOTED_IDENTIFIERS ON 陳述式。  
  
- -r *row_terminator*  
指定資料列結束字元。  
  
- -R  
指定要使用定義給用戶端電腦地區設定的區域格式，將貨幣、日期和時間資料大量複製到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中。  
  
- -S *server*  
指定要連線之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱，或者，如果使用了 -D，則為 DSN。  
  
- -t *field_terminator*  
指定欄位結束字元。  
  
- -T  
指定 `bcp` 公用程式使用信任連線 (整合式安全性) 連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
- -U *login_id*  
指定用來連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的登入識別碼。  
  
- -v  
報告 `bcp` 公用程式版本號碼和著作權。  
  
- -w  
使用 Unicode 字元執行大量複製作業。  
  
在此版本中，支援 Latin-1 和 UTF-16 字元。  
  
## <a name="unavailable-options"></a>無法使用的選項
在目前版本中，下列語法和選項無法使用：  

- -c  
指定資料檔案中之資料的字碼頁。  
  
- -h *hint*  
指定將資料大量匯入資料表或檢視期間所使用的一或多個提示。  
  
- -i *input_file*  
指定回應檔案的名稱。  
  
- -N  
對於非字元資料，使用資料的原生 (資料庫) 資料類型；如果是字元資料，則使用 Unicode 字元。  
  
- -o *output_file*  
指定接收來自命令提示字元重新導向之輸出的檔案名稱。  
  
- -V (80 | 90 | 100)  
使用舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的資料類型。  
  
- -X  
與 format 和 -f format_file 選項一起使用，會產生以 XML 為基礎的格式檔案，而非預設的非 XML 格式檔案。  
  
## <a name="see-also"></a>另請參閱

[使用 **sqlcmd** 進行連線](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
