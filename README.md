#include "Actor.h"
#include "GraphObject.h"
#include "GameWorld.h"
#include "StudentWorld.h"
#include "GameConstants.h"



Actor::Actor(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world)
	: GraphObject(imageID, startX, startY, dir, size, depth), m_world(world)
{
	m_alive = true;
	setVisible(true);
}

Actor::~Actor()
{}
// Students:  Add code to this file (if you wish), Actor.h, StudentWorld.h, and StudentWorld.cpp

StudentWorld* Actor::getWorld()
{
	return m_world;
}

bool Actor::isAlive()
{
	return m_alive;
}

void Actor::makeDead()
{
	delete this;
}


Dirt::Dirt(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world)
	: Actor(IID_DIRT, startX, startY, dir, 0.25, 3, world)
{}

Dirt::~Dirt()
{}

void Dirt::doSomething()
{}

void Dirt::getAnnoyed()
{}


Person::Person(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world, int health)
	:Actor(imageID, startX, startY, dir, size, depth, world), m_health(health)
{}

Person::~Person()
{}

int Person::health()
{
	return m_health;
}


Frackman::Frackman(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, StudentWorld* world, int health)
	:Person(IID_PLAYER, 30, 60, right, 1, 0, world, 10)
{}

Frackman::~Frackman()
{}

void Frackman::doSomething()
{
	if (!isVisible())
		return;
	int ch;
	if (getWorld()->getKey(ch) == true)
	{
		// user hit a key this tick!
		switch (ch)
		{
		case KEY_PRESS_LEFT:
			if (getDirection() != left)
			{
				setDirection(left);
				break;
			}
			else
			{
				if (getX() > 0)
				{
					moveTo(getX() - 1, getY());
				}
				else
					moveTo(getX(), getY());
				break;
			}
		case KEY_PRESS_RIGHT:
			if (getDirection() != right)
			{
				setDirection(right);
				break;
			}
			else
			{
				if (getX() < 60)
				{
					moveTo(getX() + 1, getY());
				}
				else
					moveTo(getX(), getY());
				break;
			}
		case KEY_PRESS_UP:
			if (getDirection() != up)
			{
				setDirection(up);
				break;
			}
			else
			{
				if (getY() < 60)
				{
					moveTo(getX(), getY() + 1);
				}
				else
					moveTo(getX(), getY());
				break;
			}
		case KEY_PRESS_DOWN:
			if (getDirection() != down)
			{
				setDirection(down);
				break;
			}
			else
			{
				if (getY() > 0)
				{
					moveTo(getX(), getY() - 1);
				}
				else
					moveTo(getX(), getY());
				break;
			}
		default:
			return;
		}
		for (int i = getX(); i < getX() + 4; i++)
		{
			for (int j = getY(); j < getY() + 4; j++)
			{
				if (getWorld()->isDirt(i, j))
				{
					getWorld()->removeDirt(i, j);
				}
			}
		}
	}
}

void Frackman::getAnnoyed()
{}
