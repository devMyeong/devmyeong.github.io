---
title:  "Gof Design Pattern"

categories:
  - Design Pattern
tags:
  - []

comments: true

toc: true
toc_sticky: true

date: 2021-08-25
last_modified_at: 2021-08-25
---

## Chapter 00 스트래티지 패턴

### 00-1 스트래티지 패턴 (Strategy Pattern)

```cpp
//----------------------------------------------------------------------------------------------------------------
// 스트래티지 패턴이란 여러 알고리즘을 하나의 추상적인 접근점을 만들어 접근 점에서 서로 교환 가능하도록 하는 패턴
//----------------------------------------------------------------------------------------------------------------

#include "stdafx.h"

class Weapon {
public:
	Weapon() {}
	virtual ~Weapon() {}

public:
	virtual void Attack() {}
};

class Knife : public Weapon
{
	// Weapon을(를) 통해 상속됨
	virtual void Attack() override
	{
		cout << "칼 공격" << endl;
	}
};

class Sword : public Weapon
{
	// Weapon을(를) 통해 상속됨
	virtual void Attack() override
	{
		cout << "검 공격" << endl;
	}
};

class Player
{
	// 접근점
private:
	Weapon* m_weapon;

public:
	Player() : m_weapon(nullptr) {}
	virtual ~Player() {}

	// 교환 가능
public:
	void setWeapon(Weapon* weapon)
	{
		m_weapon = weapon;
	}

	void Attack()
	{
		if (m_weapon == nullptr)
		{
			cout << "맨손 공격" << endl;
		}
		else
		{
			// 델리게이트 : 델리게이트란 특정 객체의 기능을 사용하기 위해 다른 객체의 기능을 호출하는 것
			m_weapon->Attack();
		}

	}
};

void main()
{
	Player* player = new Player();
	player->Attack();

	// new Knife()를 해줬으니 메모리 해제를 해줘야 하지만 생략한다
	player->setWeapon(new Knife());
	player->Attack();

	// new Sword()를 해줬으니 메모리 해제를 해줘야 하지만 생략한다
	player->setWeapon(new Sword());
	player->Attack();

	delete player;
	player = nullptr;
}
```

<br>

## Chapter 01 어댑터 패턴

### 01-1 어댑터 패턴(Adapter Pattern)

```cpp
//-------------------------------------------------------------------------
// 어댑터 패턴을 활용하면 연관성 없는 두 객체를 묶어 사용할 수 있다
// 어댑터 패턴을 활용하면 주어진 알고리즘을 요구사항에 맞춰 사용할 수 있다
// 아래 코드에서는 주어진 알고리즘을 Math로 가정
//-------------------------------------------------------------------------

#include "stdafx.h"

class Math
{
public:
	Math() {}
	virtual ~Math() {}

public:
	// 두배
	double twoTime(double num) { return num * 2; }

	// 절반
	double half(double num) { return num / 2; }

	// 강화된 알고리즘
	double doubled(double d) { return d * 2; }

};

class Adapter
{
public:
	Adapter() {}
	virtual ~Adapter() {}

	// 원하는 기능
public:
	virtual float	twiceOf(float f) = 0;
	virtual float	halfOf(float f) = 0;

};

class AdapterImpl : public Adapter
{
public:
	AdapterImpl() {}
	virtual ~AdapterImpl() {}

	// 원하는 기능
public:
	float twiceOf(float f)
	{
		// Math 알고리즘을 바로 사용할 수 없어서 구현체에서
		// 주어진 알고리즘을 사용할 수 있게 변경해준다
		//return (float) Math().twoTime((double)f);
		return (float)Math().doubled((double)f);
	}
	float halfOf(float f)
	{
		cout << "절반 함수 호출 시작" << endl;
		return (float)Math().half((double)f);
	}

};

void main()
{
	Adapter* adapter = new AdapterImpl();

	cout << adapter->twiceOf((float)100.0) << endl;
	cout << adapter->halfOf((float)80.0) << endl;

	delete adapter;
	adapter = nullptr;

}
```

<br>

## Chapter 02 템플릿 메소드 패턴

### 02-1 템플릿 메소드 패턴(Template Method Pattern)

```cpp
//----------------------------------------------
// 알고리즘의 구조를 메소드에 정의하고
// 하위 클래스에서 알고리즘 구조의
// 변경없이 알고리즘을 재정의 하는 패턴
//----------------------------------------------

#include "stdafx.h"
#include<string>

class GameConnectHelper
{
public:
	GameConnectHelper() {}
	virtual ~GameConnectHelper() {}

	// 외부에는 노출되면 안되고 하위 클래스 에서는 사용할 수 있어야 하는 알고리즘들
protected:
	virtual string doSecurity(string string) = 0;
	virtual bool authentication(string id, string password) = 0;
	virtual int authorization(string userName) = 0;
	virtual string connection(string info) = 0;

public:
	// 템플릿 메소드
	string requestConnection(string str)
	{
		// 보안 작업 -> 암호화 된 문자열을 복호화
		string decodedInfo = doSecurity(str);

		// 반환된 것을 가지고 아이디, 암호를 할당한다
		string id = "aaa";
		string password = "bbb";

		if (authentication(id, password) == false)
		{
			cout << "예외 처리 작업" << endl;
			cout << "아이디 암호 불일치" << endl;
		}

		string userName = "userName";
		int i = authorization(userName);

		switch (i)
		{
		case 0:
			cout << "게임 매니저" << endl;
			break;
		case 1:
			cout << "유료 회원" << endl;
			break;
		case 2:
			cout << "무료 회원" << endl;
			break;
		case 3:
			cout << "권한 없음" << endl;
			break;
		default:
			cout << "기타 상황" << endl;
			break;
		}

		return connection(decodedInfo);
	}

};

class DefaultGameConnectHelper : public GameConnectHelper
{
public:
	DefaultGameConnectHelper() {}
	virtual ~DefaultGameConnectHelper() {}

	// GameConnectHelper을(를) 통해 상속됨
	virtual string doSecurity(string string) override
	{
		cout << "디코드" << endl;
		return string;
	}
	virtual bool authentication(string id, string password) override
	{
		cout << "아이디/암호 확인 과정" << endl;
		return true;
	}
	virtual int authorization(string userName) override
	{
		// 셧다운제가 생겨서 청소년의 접속을 막아야 한다면
		// 이 함수에서 권한 확인을 한 뒤 청소년에 해당하는
		// 코드를 return 하면 된다
		cout << "권한 확인" << endl;
		return 0;
	}
	virtual string connection(string info) override
	{
		// 이 단계에서는 접속단계 에서 필요한 정보들을 넘겨준다
		cout << "마지막 접속단계!" << endl;
		return info;
	}
};

void main()
{
	GameConnectHelper* helper = new DefaultGameConnectHelper();

	helper->requestConnection("아이디 암호 등 접속 정보");

	delete helper;
	helper = nullptr;
}
```

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}