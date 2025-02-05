---
title: '빠른 시작: Python을 사용하여 연결 - Azure Database for MySQL'
description: 이 빠른 시작에서는 MySQL용 Azure Database에서 데이터를 연결하고 쿼리하는 데 사용할 수 있는 몇 가지 Python 코드 샘플을 제공합니다.
author: savjani
ms.author: pariks
ms.service: mysql
ms.custom:
- mvc
- seo-python-october2019
- devx-track-python
ms.devlang: python
ms.topic: quickstart
ms.date: 10/28/2020
ms.openlocfilehash: a4391ecb7175b0e473b47cc3de43fd113795bc6b
ms.sourcegitcommit: a67b972d655a5a2d5e909faa2ea0911912f6a828
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104889028"
---
# <a name="quickstart-use-python-to-connect-and-query-data-in-azure-database-for-mysql"></a>빠른 시작: Python을 사용하여 Azure Database for MySQL에서 데이터 연결 및 쿼리

이 빠른 시작에서는 Python을 사용하여 Azure Database for MySQL에 연결합니다. 그런 다음, SQL 문을 사용하여 Mac, Ubuntu Linux 및 Windows 플랫폼에서 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제합니다. 

## <a name="prerequisites"></a>사전 요구 사항
이 빠른 시작에는 다음이 필요합니다.

- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free).
- [Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)을 사용하여 Azure Database for MySQL 단일 서버 만들기 <br/> 또는 [Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)를 만듭니다(없는 경우).
- 퍼블릭 또는 프라이빗 액세스를 사용하는지 여부에 따라 아래 작업 중 **하나** 를 완료하여 연결을 활성화합니다.

   |작업| 연결 방법|방법 가이드|
   |:--------- |:--------- |:--------- |
   | **방화벽 규칙 구성** | 공용 | [포털](./howto-manage-firewall-using-portal.md) <br/> [CLI](./howto-manage-firewall-using-cli.md)|
   | **서비스 엔드포인트 구성** | 공용 | [포털](./howto-manage-vnet-using-portal.md) <br/> [CLI](./howto-manage-vnet-using-cli.md)| 
   | **프라이빗 링크 구성** | Private | [포털](./howto-configure-privatelink-portal.md) <br/> [CLI](./howto-configure-privatelink-cli.md) | 

- [데이터베이스 및 비관리 사용자 만들기](./howto-create-users.md)

## <a name="install-python-and-the-mysql-connector"></a>Python 및 MySQL 커넥터 설치

다음 단계를 사용하여 컴퓨터에 Python과 Python용 MySQL 커넥터를 설치합니다. 

> [!NOTE]
> 이 빠른 시작에서는 [MySQL 커넥터/Python 개발자 가이드](https://dev.mysql.com/doc/connector-python/en/)를 사용합니다.

1. OS에 대한 [Python 3.7 이상](https://www.python.org/downloads/)을 다운로드하여 설치합니다. MySQL 커넥터를 사용하려면 `PATH`에 Python을 추가해야 합니다.
   
2. 명령 프롬프트 또는 `bash` 셸을 열고 대문자 V 스위치를 사용하여 `python -V`를 실행하여 Python 버전을 확인합니다.
   
3. `pip` 패키지 설치 관리자는 최신 버전의 Python에 포함되어 있습니다. `pip install -U pip`를 실행하여 최신 버전으로 `pip`를 업데이트합니다. 
   
   `pip`가 설치되지 않은 경우 `get-pip.py`를 사용하여 다운로드하고 설치할 수 있습니다. 자세한 내용은 [설치](https://pip.pypa.io/en/stable/installing/)를 참조하세요. 
   
4. `pip`를 사용하여 Python용 MySQL 커넥터 및 해당 종속성을 설치합니다.
   
   ```bash
   pip install mysql-connector-python
   ```
   
[문제가 있나요? 알려주세요.](https://aka.ms/mysql-doc-feedback)

## <a name="get-connection-information"></a>연결 정보 가져오기

Azure Portal에서 Azure Database for MySQL에 연결하는 데 필요한 연결 정보를 가져옵니다. 서버 이름, 데이터베이스 이름 및 로그인 자격 증명이 필요합니다.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
   
1. 포털 검색 창에서 **mydemoserver** 와 같이 만든 Azure Database for MySQL 서버를 검색하여 선택합니다.
   
   :::image type="content" source="./media/connect-python/1_server-overview-name-login.png" alt-text="MySQL용 Azure Database 서버 이름":::
   
1. 서버의 **개요** 패널에 있는 **서버 이름** 과 **서버 관리자 로그인 이름** 을 기록해 둡니다. 암호를 잊어버리면 이 페이지에서 암호를 재설정할 수 있습니다.
   
   :::image type="content" source="./media/connect-python/azure-database-for-mysql-server-overview-name-login.png" alt-text="Azure Database for MySQL 서버 이름 2":::

## <a name="step-1-create-a-table-and-insert-data"></a>1단계: 테이블 만들기 및 데이터 삽입

다음 코드를 사용하여 서버 및 데이터베이스에 연결하고, 테이블을 만들고, **INSERT** SQL 문을 사용하여 데이터를 로드합니다. 이 코드는 mysql.connector 라이브러리를 가져오고 다음 메서드를 사용합니다.
- 구성 컬렉션의 [인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)를 사용하여 Azure Database for MySQL에 연결하는 [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수. 
- [cursor.execute](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다. 
- 커서 사용을 마쳤을 경우 [cursor.close()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-close.html).
- [conn.close()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlconnection-close.html): 연결을 닫습니다.

> [!IMPORTANT]
> - SSL은 기본적으로 활성화되어 있습니다. 로컬 환경에서 연결하려면 [DigiCertGlobalRootG2 SSL 인증서](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)를 다운로드해야 할 수도 있습니다.
> - `<mydemoserver>`, `<myadmin>`, `<mypassword>` 및 `<mydatabase>` 자리 표시자를 MySQL 서버 및 데이터베이스의 값으로 바꿉니다.

```python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'<mydemoserver>.mysql.database.azure.com',
  'user':'<myadmin>@<mydemoserver>',
  'password':'<mypassword>',
  'database':'<mydatabase>',
  'client_flags': [mysql.connector.ClientFlag.SSL],
  'ssl_ca': '/var/wwww/html/DigiCertGlobalRootG2.crt.pem'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

[문제가 있나요? 알려주세요.](https://aka.ms/mysql-doc-feedback)

## <a name="step-2-read-data"></a>2단계: 데이터 읽기

**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요. 이 코드는 mysql.connector 라이브러리를 가져오고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드를 사용하여 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다. 

이 코드는 [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) 메서드를 사용하여 데이터 행을 읽고, 결과 세트를 컬렉션 행에 보관하고, `for` 반복기를 사용하여 행을 반복합니다.

```python
  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

```

## <a name="step-3-update-data"></a>3단계: 데이터 업데이트

**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요. 이 코드는 mysql.connector 라이브러리를 가져오고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드를 사용하여 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다. 

```python
  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")
```

## <a name="step-4-delete-data"></a>4단계: 데이터 삭제

다음 코드를 사용하여 데이터를 연결하고 **DELETE** SQL 문을 통해 데이터를 제거합니다. 이 코드는 mysql.connector 라이브러리를 가져오고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드를 사용하여 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다. 

```python

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")
```

## <a name="clean-up-resources"></a>리소스 정리

이 빠른 시작에서 사용된 모든 리소스를 정리하려면 다음 명령을 사용하여 리소스 그룹을 삭제합니다.

```azurecli
az group delete \
    --name $AZ_RESOURCE_GROUP \
    --yes
```

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [포털을 사용하여 Azure Database for MySQL 서버 관리](./howto-create-manage-server-portal.md)<br/>

> [!div class="nextstepaction"]
> [CLI를 사용하여 Azure Database for MySQL 서버 관리](./how-to-manage-single-server-cli.md)

[원하는 항목을 찾을 수 없나요? 알려주세요.](https://aka.ms/mysql-doc-feedback)
