# NASA-Space-App-Challenge-Final-Codes
Game manager
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class gameManager : MonoBehaviour
{

    public float slowFactorRate = 10f;
    public float deadFactorRate = 10f;
    public int lifeOfPlayer = 3;
    public GameObject life1;
    public GameObject life2;
    public GameObject life3;
    //public GameObject gameoverscreen;
    public bool ispaused = false;
    public float pausedelay = 10f;

    private void Start()
    {
        Time.timeScale = 1f;
        ispaused = false;
        life1.SetActive(true);
        life2.SetActive(true);
        life3.SetActive(true);
    }

    public void decreaseLife()
    {
        if (lifeOfPlayer == 3)
        {
            life2.SetActive(false);
        }
        if (lifeOfPlayer == 2)
        {
            life2.SetActive(false);
            life1.SetActive(false);
        }
        if (lifeOfPlayer == 1)
        {
            life3.SetActive(false);
            life2.SetActive(false);
            life1.SetActive(false);
        }

        if (lifeOfPlayer <= 1)
        {
            CameraShake.shouldShake = false;
            FindObjectOfType<hurtFrame>().OffHurtIndicator();
            // StartCoroutine(pauseDelay());
            //StartCoroutine(slowDownTimeWhenIsDead());
            //gameoverscreen.SetActive(true);
            SceneManager.LoadScene("GameOver");
            // Debug.Log("Game Over");


            PauseGame();

        }
        else
        {
            lifeOfPlayer--;

            StartCoroutine(slowDownTimeWhenCollides());
            //Debug.Log(lifeOfPlayer);

        }
    }
    public void IncreaseLife()
    {
        
        if (lifeOfPlayer < 3)
        {
            if (lifeOfPlayer == 2)
            {
                life1.SetActive(true);
                life2.SetActive(true);
                life3.SetActive(true);

            }
            if (lifeOfPlayer == 1)
            {
                life1.SetActive(true);
                life3.SetActive(true);

            }
            lifeOfPlayer++;
        }
        



    }

    IEnumerator slowDownTimeWhenCollides()
    {
        Time.timeScale = 1f / slowFactorRate;
        Time.fixedDeltaTime = Time.fixedDeltaTime / slowFactorRate;

        yield return new WaitForSeconds(0.5f / slowFactorRate);

        Time.timeScale = 1f;
        Time.fixedDeltaTime = Time.fixedDeltaTime * slowFactorRate;
    }

    IEnumerator slowDownTimeWhenIsDead()
    {
        Time.timeScale = 1f / slowFactorRate;
        Time.fixedDeltaTime = Time.fixedDeltaTime / deadFactorRate;

        yield return new WaitForSeconds(1f / slowFactorRate);

        Time.timeScale = 1f;
        Time.fixedDeltaTime = Time.fixedDeltaTime * deadFactorRate;
       
        // SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex + 1);
    }

    private void PauseGame()
    {
        if (ispaused)
        {
            Time.timeScale = 1;
            ispaused = false;
        }
        else
        {
            Time.timeScale = 0;
            ispaused = true;
        }
    }


    IEnumerator pauseDelay()
    {
        yield return new WaitForSeconds(2f / slowFactorRate);
    }

    

}
