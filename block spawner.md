# NASA-Space-App-Challenge-Final-Codes
code for spawning different objects
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BlockSpawner : MonoBehaviour {
	public Transform[] SpawnPoints;
	public GameObject blockprefab;
	private float timetospawn = 2f;
	public float timebetweenwaves=1f;
	public float upwardspeed=5f;
    public float wavecount = 0f;
	// Use this for initialization
	void Start () {

        wavecount = 0f;
	}
	
	// Update is called once per frame
	void Update () {
		if (Time.time >= timetospawn) {
			SpawnBlocks ();
            wavecount++;
           // Debug.Log(wavecount);

            timetospawn = Time.time + timebetweenwaves;
		}


        if (transform.position.y < -5)
        {
            Destroy(this.gameObject);
        }
        //constantly go up
        transform.position += transform.up * Time.deltaTime * upwardspeed;


	}

	void SpawnBlocks(){
		int randomIndex = Random.Range (0, SpawnPoints.Length);
		for (int i = 0; i < SpawnPoints.Length; i++) {
			if (randomIndex == i) {
				Instantiate (blockprefab,SpawnPoints[i].position,Quaternion.identity);

               // Destroy(blockprefab, 2f);
			}
		}
        
    }
  
    void PosChange(){

	}
}
