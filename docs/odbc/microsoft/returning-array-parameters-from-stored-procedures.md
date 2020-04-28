---
title: 從預存程式傳回陣列參數 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292858"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>從預存程序傳回陣列參數
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 在 Oracle 7.3 中，沒有任何方法可以存取 pl/sql 記錄類型，但 PL/SQL 程式除外。 如果封裝的程式或函式具有定義為 PL/SQL 記錄類型的正式引數，就無法將該正式引數系結為參數。 使用 Microsoft ODBC Driver for Oracle 中的 PL/SQL 資料表類型，從包含正確逸出序列的程式叫用陣列參數。  
  
 若要叫用程式，請使用下列語法：  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  要求\<的最大記錄> 參數必須大於或等於結果集中出現的資料列數目。 否則，Oracle 會傳回由驅動程式傳遞給使用者的錯誤。  
>   
>  PL/SQL 記錄不能當做陣列參數使用。 每個陣列參數只能表示資料庫資料表的一個資料行。  
  
 下列範例會定義一個封裝，其中包含兩個會傳回不同結果集的程式，然後提供兩種方法來從封裝傳回結果集。  
  
## <a name="package-definition"></a>套件定義：  
  
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
  
#### <a name="to-invoke-procedure-proc1"></a>若要叫用程式 PROC1  
  
1.  傳回單一結果集中的所有資料行：  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  以單一結果集的形式傳回每個資料行：  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     這會傳回三個結果集，每個資料行各一個。  
  
#### <a name="to-invoke-procedure-proc2"></a>若要叫用程式 PROC2  
  
1.  傳回單一結果集中的所有資料行：  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  以單一結果集的形式傳回每個資料行：  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 請確定您的應用程式會使用[SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API 來提取所有結果集。 如需詳細資訊，請參閱*ODBC 程式設計人員參考*。  
  
> [!NOTE]  
>  在 Oracle 2.0 版的 ODBC 驅動程式中，傳回 PL/SQL 陣列的 Oracle 函數不能用來傳回結果集。
