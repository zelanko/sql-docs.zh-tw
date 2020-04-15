---
title: 從儲存過程返回陣列參數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc998dadc0e0c4a4bfe054bfd1d40296bc176393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292858"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>從預存程序傳回陣列參數
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 在 Oracle 7.3 中,除了從 PL/SQL 程式之外,無法存取 PL/SQL 記錄類型。 如果打包的過程或函數具有定義為 PL/SQL 記錄類型的正式參數,則無法將該正式參數綁定為參數。 使用 Oracle 的 Microsoft ODBC 驅動程式中的 PL/SQL TABLE 類型從包含正確轉義序列的過程調用陣列參數。  
  
 要呼叫該過程,請使用以下語法:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  \<請求的>參數的最大值必須大於或等於結果集中存在的行數。 否則,Oracle 將返回驅動程式傳遞給使用者的錯誤。  
>   
>  PL/SQL 記錄不能用作數位參數。 每個陣列參數只能表示資料庫表的一列。  
  
 下面的示例定義一個包,其中包含兩個返回不同結果集的過程,然後提供了從包返回結果集的兩種方法。  
  
## <a name="package-definition"></a>套件定義:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>呼叫程序 PROC1  
  
1.  傳回單結果集中所有列:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  將每列作為單結果集傳回:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     這將返回三個結果集,每個列一個。  
  
#### <a name="to-invoke-procedure-proc2"></a>呼叫程序 PROC2  
  
1.  傳回單結果集中所有列:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  將每列作為單結果集傳回:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 確保應用程式使用[SQLMoreResult](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API 獲取所有結果集。 有關詳細資訊,請參閱*ODBC 程式者的參考*。  
  
> [!NOTE]  
>  在 Oracle 版本 2.0 的 ODBC 驅動程式中,傳回 PL/SQL 陣列的 Oracle 函數不能用於返回結果集。
