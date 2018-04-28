---
title: 連接 bcp |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: badff319d1ae969d14fc14fc68d40fdd57b776eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-with-bcp"></a>連接 bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[Bcp](http://go.microsoft.com/fwlink/?LinkID=190626)公用程式位於[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 及 macOS 上。 此頁面文件的 Windows 版本在差異`bcp`。
  
- 欄位結束字元是定位字元 ("\t")。  
  
- 行結束字元是新行字元 ("\n")。  
  
- 字元模式是慣用的格式為`bcp`格式化檔案，以及不含擴充的字元的資料檔案。  
  
> [!NOTE]  
> 反斜線 '\\' 上的命令列引數必須是加上引號或逸出。 例如，若要指定新行字元做為自訂的資料列結束字元，您必須使用下列機制的其中一個：  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
以下是範例命令引動過程的`bcp`資料表資料列複製到文字檔案：  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>可用的選項
在目前版本中，下列語法和選項可用：  

[*資料庫 ***。**]* 結構描述***。***資料表 ***中** *data_file* | **出** *data_file*

- -a *packet_size*  
指定伺服器所收送之每個網路封包的位元組數。  
  
- -b *batch_size*  
指定每一批次匯入資料的資料列數。  
  
- -c  
使用字元資料類型。  
  
- -d *database_name*  
指定要連接的資料庫。  
  
- -d  
傳遞給的值會導致`bcp`-S 選項可解譯為資料來源名稱 (DSN)。 如需詳細資訊，請參閱 「 sqlcmd 和 bcp 中的 DSN 支援 」[使用 sqlcmd 連接](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)。  
  
- -e *error_file*指定用來儲存任何的錯誤檔的完整路徑的資料列`bcp`公用程式無法從檔案傳送到資料庫。  
  
- -e  
將匯入之資料檔案中的識別值用於識別欄位。  
  
- -f *format_file*  
指定格式檔的完整路徑。  
  
- -F *first_row*  
指定要從資料表匯出或從資料檔案匯入之第一個資料列的號碼。  
  
- -k  
指定空白資料行在作業過程中應保持 Null 值，而非保有插入之資料行的任何預設值。  
  
- -l  
指定登入逾時。 – L 選項指定的登入之前的秒數[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]逾時當您嘗試連接到伺服器。 預設登入逾時是 15 秒。 登入逾時必須是介於 0 到 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`bcp` 就會產生錯誤訊息。 值為 0 會指定無限逾時。
  
- -L *last_row*  
指定要從資料表匯出或從資料檔案匯入的最後一個資料列的號碼。  
  
- -m *max_errors*  
指定最大數目之前可發生的語法錯誤`bcp`取消作業。  
  
- -n  
使用資料的原生 (資料庫) 資料類型來執行大量複製作業。  
  
- -P *password*  
指定登入識別碼的密碼。  
  
- -Q  
在 `bcp` 公用程式與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 執行個體之間的連接中，執行 SET QUOTED_IDENTIFIERS ON 陳述式。  
  
- -r *row_terminator*  
指定資料列結束字元。  
  
- -r  
指定要使用定義給用戶端電腦地區設定的區域格式，將貨幣、日期和時間資料大量複製到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中。  
  
- -S *server*  
指定的名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體連線，或如果-D 是使用，資料來源名稱。  
  
- -t *field_terminator*  
指定欄位結束字元。  
  
- -T  
指定`bcp`公用程式連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]信任連接 （整合式安全性）。  
  
- -U *login_id*  
指定用來連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的登入識別碼。  
  
- -v  
報告 `bcp` 公用程式版本號碼和著作權。  
  
- -w  
使用 Unicode 字元執行大量複製作業。  
  
在此版本中，支援 Latin-1 和 UTF-16 字元。  
  
## <a name="unavailable-options"></a>無法使用的選項
在目前版本中，下列語法和選項即無法使用：  

- -c  
指定資料檔案中之資料的字碼頁。  
  
- -h *hint*  
指定將資料大量匯入資料表或檢視期間所使用的一或多個提示。  
  
- -i *input_file*  
指定回應檔案的名稱。  
  
- -n  
對於非字元資料，使用資料的原生 (資料庫) 資料類型；如果是字元資料，則使用 Unicode 字元。  
  
- -o *output_file*  
指定接收來自命令提示字元重新導向之輸出的檔案名稱。  
  
- -V (80 | 90 | 100)  
使用資料類型，從較早版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
- -X  
與 format 和 -f format_file 選項一起使用，會產生以 XML 為基礎的格式檔案，而非預設的非 XML 格式檔案。  
  
## <a name="see-also"></a>另請參閱

[使用連接**sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
