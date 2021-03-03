# How-to-spawn-a-prefab-that-follows-a-path-of-nodes-unity-
Hello, I am trying to create a tower defense game and everything has worked smoothly so far except for the fact that I can't Destroy the enemy as it hits the death zone causing more than one damage to take place. Also it boggs down the system that I am using because of the high amounts of GameObjects. I am trying to find a solution that involves making the enemy a prefab that I can just instantiate. However I have tried many different things and most of the time it just breaks the game. I have my code attached as well as the editor view. If anyone could help it would be greatly appreciated! 
Hello, I am trying to create a tower defense game and everything has worked smoothly so far except for the fact that I can't Destroy the enemy as it hits the death zone causing more than one damage to take place. Also it boggs down the system that I am using because of the high amounts of GameObjects. I am trying to find a solution that involves making the enemy a prefab that I can just instantiate. However I have tried many different things and most of the time it just breaks the game. I have my code attached as well as the editor view. If anyone could help it would be greatly appreciated!
Code (CSharp):
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
 
public class PathFollower : MonoBehaviour
{
    public GameObject[] nodes;
    private int currentNode = 0;
    private float lastNodeSwitchTime;
    public float speed = 1.0f;
 
    public void Start()
    {
        lastNodeSwitchTime = Time.time;
    }
 
    public void Update()
    {
        Vector3 startPosition = nodes[currentNode].transform.position;
        Vector3 endPosition = nodes[currentNode + 1].transform.position;
        float pathLength = Vector3.Distance(startPosition, endPosition);
        float totalTimeOnPath = pathLength / speed;
        float currentTimeOnPath = Time.time - lastNodeSwitchTime;
        gameObject.transform.position = Vector2.Lerp(startPosition, endPosition, currentTimeOnPath / totalTimeOnPath);
        if (gameObject.transform.position.Equals(endPosition))
        {
            if (currentNode <  nodes.Length - 2)
            {
                currentNode++;
                lastNodeSwitchTime = Time.time;
            }
        }
    }
}
