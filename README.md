# Darg-and-drop-in-unity

using UnityEngine;
using System.Collections;
using UnityEngine.UI;


public class  Drag_main_2_4800186: MonoBehaviour
{
		
	public Vector3 screenSpace;
	public Vector3 offSet;
	public Vector3 curScreenSpace;
	public Vector3 curPosition;

	public GameObject ss0 ,x_dot, x_dot2, y_dot, y_dot2;
	public AR_Object_OrbitJava orbit;
	public Text x_value;//, x1_val, y1_val;

	public GameObject Text_obj;
	public main_obj_sc_4800186 line;
	//public Text x_value, x1_val, y1_val, a1_val, b1_val;
	public float yy1;

	public Vector3 storeSoundposition;
	//public AudioSource sld;

	public AR_AudioSourseManagerScript snd;

	void Start ()
	{
		//ss0.transform.localPosition = new Vector3 (0.5f, 0.5f, 0);
		orbit = GameObject.FindObjectOfType (typeof(AR_Object_OrbitJava)) as AR_Object_OrbitJava;
		snap ();
		line.Update1 ();
	
	}

	void OnMouseDown1 ()
	{
		orbit.enabled = false;
		screenSpace = Camera.main.WorldToScreenPoint (transform.position);
		offSet = transform.position - Camera.main.ScreenToWorldPoint (new Vector3 (Input.mousePosition.x, Input.mousePosition.y, screenSpace.z));		
		dragit = true;
		U = true;
	
//		sspace = Camera.main.WorldToScreenPoint (transform.position);
//		oset = transform.position - Camera.main.ScreenToWorldPoint (new Vector3 (Input.mousePosition.x, Input.mousePosition.y, sspace.z));
	}

	void OnMouseDrag1 ()
	{	
		transform.position = Camera.main.ScreenToWorldPoint (new Vector3 (Input.mousePosition.x, Input.mousePosition.y, screenSpace.z)) + offSet;		
		transform.localPosition = new Vector3 (transform.localPosition.x, transform.localPosition.y, 0);	
		if (transform.localPosition.x > x_dot.transform.localPosition.x) {				
			transform.localPosition = new Vector3 (x_dot.transform.localPosition.x, transform.localPosition.y, 0);
		} else if (transform.localPosition.x < x_dot2.transform.localPosition.x) {				
			transform.localPosition = new Vector3 (x_dot2.transform.localPosition.x, transform.localPosition.y, 0);
		}

		if (transform.localPosition.y > y_dot.transform.localPosition.y) {				
			transform.localPosition = new Vector3 (transform.localPosition.x, y_dot.transform.localPosition.y, 0);
		} else if (transform.localPosition.y < y_dot2.transform.localPosition.y) {				
			transform.localPosition = new Vector3 (transform.localPosition.x, y_dot2.transform.localPosition.y, 0);
		}
		if(storeSoundposition!= transform.position)
		{
			//sld.Play ();
			snd.sfxSource [0].Play ();
			storeSoundposition=transform.position;
		}
		snap ();
	}

	void OnMouseUp1 ()
	{
	
		orbit.enabled = true;
			
		snap ();
			
	}


	void snap ()
	{
	
		float x1 = ss0.transform.localPosition.x;
		float y1 = ss0.transform.localPosition.y;			
		x1 = Mathf.Round (x1 / 0.1f);
		y1 = Mathf.Round (y1 / 0.1f);
		ss0.transform.localPosition = new Vector3 (x1 * 0.1f, y1 * 0.1f, 0);

		if (y1 >= 1) {
		
			Text_obj.transform.localPosition = new Vector3 (Text_obj.transform.localPosition.x, 1.1f, Text_obj.transform.localPosition.z);
		//	cw.transform.localPosition = new Vector3 (cw.transform.localPosition.x, -2.5f, cw.transform.localPosition.z);

		} else if (y1 <= -1) {
			Text_obj.transform.localPosition = new Vector3 (Text_obj.transform.localPosition.x, -2.5f, Text_obj.transform.localPosition.z);
		} else if (y1 == 0) {
			Text_obj.transform.localPosition = new Vector3 (Text_obj.transform.localPosition.x, -4f, Text_obj.transform.localPosition.z);
		}
	ss0.transform.localPosition = new Vector3 (x1 * 0.1f, y1 * 0.1f, 0);
	x_value.text = "B ( " + x1 * 1 + " , " + y1 * 1 + " )" + "";

	//x1_val.text = x1 * 1 + "";
	//y1_val.text = y1 * 1 + "";



		//	x_value.text = "( " + x1 * 1 + " , " + y1 * 1 + " i )" + "";
		/*x1_val.text = x1 * 1 + "";
		y1_val.text = y1 * 1 + "";

		if (y1 < 0) {
			yy1 = y1 * -1;
		} else {
			yy1 = y1;
		}

		a1_val.text = x1 * 1 + "";

		if (x1 == 0) {
			if (y1 < 0) {
				a1_val.text = "";
				b1_val.text = "- " + yy1 * 1 + "i";
				b1_val.transform.localPosition = new Vector3 (37f, b1_val.transform.localPosition.y, b1_val.transform.localPosition.z);
			} else if (y1 > 0) {
				a1_val.text = "";
				b1_val.text = yy1 * 1 + "i";
				b1_val.transform.localPosition = new Vector3 (37f, b1_val.transform.localPosition.y, b1_val.transform.localPosition.z);
			} else if (y1 == 0) {
				b1_val.text = "+ " + yy1 * 1 + "i";
				b1_val.transform.localPosition = new Vector3 (83f, b1_val.transform.localPosition.y, b1_val.transform.localPosition.z);
			} else if (y1 == 1) {
				a1_val.text = "";
				b1_val.text = "" + "+ i" + "";
				b1_val.transform.localPosition = new Vector3 (37f, b1_val.transform.localPosition.y, b1_val.transform.localPosition.z);
			}
		} else if (x1 > 0 || x1 < 0) {
			a1_val.text = x1 * 1 + "";
			b1_val.transform.localPosition = new Vector3 (83f, b1_val.transform.localPosition.y, b1_val.transform.localPosition.z);

			if (y1 < 0) {
				b1_val.text = "- " + yy1 * 1 + "i";
			} else if (y1 > 0) {
				b1_val.text = "+ " + yy1 * 1 + "i";
			} else if (y1 == 0) {
				b1_val.text = "+ " + yy1 * 1 + "i";
			} else if (y1 == 1) {
				b1_val.text = "" + "+ i" + "";
				print ("y1 :" + y1);
			}
		} else if (x1 == 0 && y1 == 0) {
			a1_val.text = x1 * 1 + "";
			b1_val.text = yy1 * 1 + "i";
		
		}*/

		line.Update1 ();
	}

     
	public RaycastHit hit;
	private bool dragit = false;
	private bool U = false;
	private Ray ray;

	void LateUpdate ()
	{
		if (Input.GetMouseButtonDown (0)) {
			ray = Camera.main.ScreenPointToRay (Input.mousePosition);
			if (Physics.Raycast (ray, out hit, 1000)) {
				if (hit.collider.name == this.name) {
					hit.collider.SendMessage ("OnMouseDown1", SendMessageOptions.DontRequireReceiver);
				}
			}
		}
		if (dragit && Input.GetMouseButton (0))
			gameObject.SendMessage ("OnMouseDrag1", SendMessageOptions.DontRequireReceiver);//d.MouseDrag();
		if (Input.GetMouseButtonUp (0)) {
			if (U) {
				gameObject.SendMessage ("OnMouseUp1", SendMessageOptions.DontRequireReceiver);
				U = false;
				dragit = false;
			}
		}
	}
}

