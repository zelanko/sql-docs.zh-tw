---
title: 模擬 Oracle 封裝變數
description: 描述 Oracle SQL Server 移轉小幫手（SSMA）如何在 SQL Server 中模擬 Oracle 封裝變數。
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 9a8ca5c7dfdda98e1c005c3851d061957cf67449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762822"
---
# <a name="emulating-oracle-package-variables"></a>模擬 Oracle 封裝變數

Oracle 支援將變數、類型、預存程式和函式封裝成封裝。 當您轉換 Oracle 封裝時，您必須轉換：

* 程式和功能-公用和私用
* 變數
* 資料指標
* 初始化常式

本文說明 Oracle 的 SQL Server 移轉小幫手（SSMA）如何將封裝變數轉換成 SQL Server。

## <a name="conversion-basics"></a>轉換基本概念

若要儲存封裝變數，SSMA for Oracle 會使用位於特殊`ssma_oracle`架構中的預存程式`ssma_oracle.db_storage`和資料表。 此資料表會依`SPID` （會話識別碼）和登入時間進行篩選。 這項篩選可讓您區分不同會話的變數。

在每個轉換的封裝程式開始時，SSMA 會呼叫`ssma_oracle.db_check_init_package`特殊程式，這會檢查封裝是否已初始化，並在需要時將它初始化。 每個初始化程式都會清除儲存體資料表，並設定每個封裝變數的預設值。

## <a name="example"></a>範例

請考慮下列轉換數個封裝變數的範例：

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

SSMA 會將它轉換成下列 Transact-sql 程式碼：

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>模擬封裝變數的 Get 和 Set 方法

Oracle 會`Get`針對`Set`封裝變數使用和方法，以避免讓其他 subprograms 直接讀取和寫入。 如果需要在相同會話中的 subprogram 呼叫之間保留一些可用的變數，這些變數就會視為全域變數。

若要克服此範圍規則，SSMA for Oracle 會針對每`ssma_oracle.set_pv_varchar`個變數類型使用像是的預存程式。 若要存取這些變數，SSMA 會使用一組與交易`get_*`無關`set_*`的和程式和函數。

| Oracle 中的資料類型 | SSMA `Set`程式           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| 日期                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

為了區別不同會話中的變數，SSMA 會儲存變數及其`SPID` （會話識別碼）和會話的登入時間。 因此`get_*` ，和`set_*`程式會讓變數與執行它們的會話保持獨立的狀態。
