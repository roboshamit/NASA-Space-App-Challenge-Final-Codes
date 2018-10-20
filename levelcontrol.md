# NASA-Space-App-Challenge-Final-Codes
Level Control script


using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class LevelControl : MonoBehaviour {

    GameObject[] toEnable, toDisable;

 
    public GameObject correctSign, incorrectSign;
    
    int currentSceneIndex;

    
    public string point = "data1Got";

    // Use this for initialization
    void Start()
    {
    
        // Getting current scene build index
        currentSceneIndex = SceneManager.GetActiveScene().buildIndex;
        
        toEnable = GameObject.FindGameObjectsWithTag("toenable");
        toDisable = GameObject.FindGameObjectsWithTag("todisable");

 
        foreach (GameObject element in toEnable)
        {
            element.gameObject.SetActive(false);
        }

    }


    public void RightAnswer()
    {

        foreach (GameObject element in toDisable)
        {
            element.gameObject.SetActive(false);
        }

        
        correctSign.gameObject.SetActive(true);
        FoodScript.food += 50;
        FuelScript.fuel += 50;
        EnergyScript.energy += 50;
        DataScript.data += 50;

        int datagot = PlayerPrefs.GetInt(point);

      
        if (datagot == 1)
            Invoke("LoadNextTask", 1f);
        else
            Invoke("GetData", 1f);
    }
    public void FoodPlus()
    {
        FoodScript.food += 50;
    }
    public void FoodMinus()
    {
        FoodScript.food -= 50;
    }
    public void FuelPlus()
    {
        FuelScript.fuel += 50;
    }
    public void FuelMinus()
    {
        FuelScript.fuel -= 50;
    }
    public void EnergyPlus()
    {
        EnergyScript.energy += 50;

    }
    public void EnergyMinus()
    {
        EnergyScript.energy -= 50;
    }
    public void Summer()
    {
        FoodScript.food -= 70;
        FuelScript.fuel -= 30;
        SceneManager.LoadScene("transportselect");
    }
    public void Winter()
    {
        FoodScript.food -= 40;
        FuelScript.fuel -= 70;
        SceneManager.LoadScene("transportselect");
    }

    public void WrongAnswer()
    {
        
        foreach (GameObject element in toDisable)
        {
            element.gameObject.SetActive(false);
        }

     
        incorrectSign.SetActive(true);
        FoodScript.food -= 50;
        FuelScript.fuel -= 50;
        EnergyScript.energy -= 50;
        DataScript.data -= 50;

        if (FoodScript.food == 0)
        {
            SceneManager.LoadScene("GameOver");
        }
        int datagot = PlayerPrefs.GetInt(point);
        if (datagot == 1)
            Invoke("LoadNextTask", 1f);
        else
            Invoke("GetData", 1f);
        //Invoke("GotoMainMenu", 1f);
    }

    void GetData()
    {
        
        correctSign.SetActive(false);

        // to store this value between the scenes
        PlayerPrefs.SetInt(point, 1);

      
        Invoke("LoadNextLevel", 1f);
    }

    void LoadNextTask()
    {
        SceneManager.LoadScene(currentSceneIndex + 1);
    }

    
    void GotoMainMenu()
    {
        SceneManager.LoadScene("MainMenu");
    }

}
