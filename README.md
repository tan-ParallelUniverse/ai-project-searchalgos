# AI-Project-SearchAlgos
Hey... 
This repository have been created for those who are curious about how search algorithms work!
# Getting Started
repository is a whole Unity Project so that contains many assets.
All the codes are stored in "/assets/scripts" folder.
For the sake of easiness I have seperated the algorithms from "Pathfinder" class and attached them in README file.
The whole Project is based on object oriented programming concept so following the code is not that hard, just a little search for methods brings you to the class that contains it.
# Stucture of scripts
Well, 

Inside the "scrips" folder there are several classes :

	- Scripts
	  - [] DemoController.cs
	  - [] Graph.cs
	  - [] GraphView.cs
	  - [] MapData.cs
	  - [] Node.cs
	  - [] NodeView.cs
	  - [x] Pathfinder.cs
	  - [] PriorityQueue.cs
	
## BFS Algorithm : Class ExpandFrontierBreadthFirst
```
void ExpandFrontierBreadthFirst(Node node)
    {
        if (node != null)
        {
            for (int i = 0; i < node.neighbors.Count; i++)
            {
                if (!m_exploredNodes.Contains(node.neighbors[i])
                    && !m_frontierNodes.Contains(node.neighbors[i]))
                {
                    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
                    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
                                                                         + (int)node.nodeType;
                    node.neighbors[i].distanceTraveled = newDistanceTraveled;

                    node.neighbors[i].previous = node;
                    node.neighbors[i].priority = m_exploredNodes.Count;

                    m_frontierNodes.Enqueue(node.neighbors[i]);
                }
            }
        }
    }
```
## Dijkastra Algorithm : Class ExpandFrontierDijkstra

```
void ExpandFrontierDijkstra(Node node)
    {
        if (node != null)
        {
            for (int i = 0; i < node.neighbors.Count; i++)
            {
                if (!m_exploredNodes.Contains(node.neighbors[i]))
                {
                    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
                    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
                                                                         + (int)node.nodeType;

                    if (float.IsPositiveInfinity(node.neighbors[i].distanceTraveled) ||
                        newDistanceTraveled < node.neighbors[i].distanceTraveled)
                    {
                        node.neighbors[i].previous = node;
                        node.neighbors[i].distanceTraveled = newDistanceTraveled;
                    }

                    if (!m_frontierNodes.Contains(node.neighbors[i]))
                    {
                        node.neighbors[i].priority = (int)node.neighbors[i].distanceTraveled;
                        m_frontierNodes.Enqueue(node.neighbors[i]);
                    }
                }
            }
        }
    }
```
## GreedyBFS Algorithm : Class ExpandFrontierGreedyBestFirst
```
void ExpandFrontierGreedyBestFirst(Node node)
    {
        if (node != null)
	{
	    for (int i = 0; i < node.neighbors.Count; i++)
	    {
		if (!m_exploredNodes.Contains(node.neighbors[i])
		    && !m_frontierNodes.Contains(node.neighbors[i]))
		{
		    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
		    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
									 + (int)node.nodeType;
		    node.neighbors[i].distanceTraveled = newDistanceTraveled;
		    node.neighbors[i].previous = node;
                    if (m_graph != null)
                    {
                        node.neighbors[i].priority = (int)m_graph.GetNodeDistance(
                            node.neighbors[i], m_goalNode);
                    }
					

		    m_frontierNodes.Enqueue(node.neighbors[i]);
		}
	    }
	}
    }
```
## AStar Algorithm : Class ExpandFrontierAStar
```
void ExpandFrontierAStar(Node node)
    {
	if (node != null)
	{
	    for (int i = 0; i < node.neighbors.Count; i++)
	    {
		if (!m_exploredNodes.Contains(node.neighbors[i]))
		{
		    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
		    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
									+ (int)node.nodeType;

		     if (float.IsPositiveInfinity(node.neighbors[i].distanceTraveled) ||
			newDistanceTraveled < node.neighbors[i].distanceTraveled)
		    {
			node.neighbors[i].previous = node;
			node.neighbors[i].distanceTraveled = newDistanceTraveled;
		    }

                    if (!m_frontierNodes.Contains(node.neighbors[i]) && m_graph != null)
		    {
                        int distanceToGoal = (int)m_graph.GetNodeDistance(node.neighbors[i], m_goalNode);
                        node.neighbors[i].priority = (int)node.neighbors[i].distanceTraveled 
                            + distanceToGoal;
			m_frontierNodes.Enqueue(node.neighbors[i]);
		    }
		}
	    }
	}
    }
```
## Authors

* **Amir Hossein Dezhbro** - *Initial work* - [tan-ParallelUniverse](https://github.com/tan-ParallelUniverse)

See also the list of [contributors](https://github.com/tan-ParallelUniverse/ai-project-searchalgos) who participated in this project.
## License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
## Acknowledgments
* the credit of this project (if there is a credit :D) goes to the ai class under supervision of prof.ghazanfari and dr.ghiasi.
