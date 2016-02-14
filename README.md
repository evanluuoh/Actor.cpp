# Actor.cpp

#include "Actor.h"
#include "StudentWorld.h"

Actor::Actor(int imageID, int startX, int startY, Direction dir = right, double size, unsigned int depth)
	: GraphObject(imageID, startX, startY, dir, size, depth)
{
	setVisible(true);
}

Actor::~Actor()
{}
// Students:  Add code to this file (if you wish), Actor.h, StudentWorld.h, and StudentWorld.cpp


Dirt::Dirt(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth)
	: Actor(IID_DIRT, startX, startY, dir, 0.25, 3)
{}

Dirt::~Dirt()
{}


Person::Person(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, int health)
	:Actor(imageID, startX, startY, dir, size, depth)
{
	m_health = health;
}

Person::~Person()
{}

int Person::health()
{
	return m_health;
}


Frackman::Frackman(int imageID, int startX, int startY, Direction dir, double size, unsigned int depth, int health)
	:Person(IID_PLAYER, 30, 60, right, 1, 0, 10)
{}

Frackman::~Frackman()
{}

void Frackman::doSomething()
{

}
