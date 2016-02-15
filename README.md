#include "Actor.h"
#include "GraphObject.h"
#include "GameWorld.h"
#include "StudentWorld.h"
#include "GameConstants.h"

Actor::Actor(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world)
	: GraphObject(imageID, startX, startY, dir, size, depth), m_world(world)
{
	setVisible(true);
}

Actor::~Actor()
{}
// Students:  Add code to this file (if you wish), Actor.h, StudentWorld.h, and StudentWorld.cpp

StudentWorld* Actor::getWorld()
{
	return m_world;
}


Dirt::Dirt(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world)
	: Actor(IID_DIRT, startX, startY, dir, 0.25, 3, getWorld())
{}

Dirt::~Dirt()
{}


Person::Person(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world, int health)
	:Actor(imageID, startX, startY, dir, size, depth, getWorld()), m_health(health)
{}

Person::~Person()
{}

int Person::health()
{
	return m_health;
}


Frackman::Frackman(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world, int health)
	:Person(IID_PLAYER, 30, 60, right, 1, 0, getWorld(), 10)
{}

Frackman::~Frackman()
{}

void Frackman::doSomething()
{
	if (health() == 0)
		return;
	int ch;
	//if ()
	if (getWorld()->getKey(ch) == true)
	{
		// user hit a key this tick!
		switch (ch)
		{
		case KEY_PRESS_LEFT:
			moveTo(getX() - 1, getY());
			break;
		case KEY_PRESS_RIGHT:
			moveTo(getX() + 1, getY());
			break;
		case KEY_PRESS_UP:
			moveTo(getX(), getY() - 1);
			break;
		case KEY_PRESS_DOWN:
			moveTo(getX(), getY() + 1);
			break;
		default:
			break;
		}
	}
}

void Frackman::getAnnoyed()
{}
