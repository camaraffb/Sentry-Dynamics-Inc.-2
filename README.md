# Sentry-Dynamics-Inc.   -   C#

/*------------------------------------------------------------------------------------------------------

PROGRAMMER:   Bakary Camara

LANGUAGE:     C# 

PLATFORM:     Microsoft Visual Studio 2012

CONCEPTS:     The goal for this project is to provide opportunity for the practice of C# program development

----------------------------------------------------------------------------------------------------------*/


using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.SqlClient;

//Code for window 1 /Login Window
namespace Finalproject
{
    public partial class Login : Form
    {
        public Login()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");

            //Admin Login
            SqlDataAdapter sda1 = new SqlDataAdapter("Select Count(*) From Login Where Username = '" + textBox1.Text + "' and Password = '" + textBox2.Text + "'  and Permissions =  1", con);
            DataTable dt = new DataTable();
            sda1.Fill(dt);

            //Janitor Login
            SqlDataAdapter sda2 = new SqlDataAdapter("Select Count(*) From Login Where Username = '" + textBox1.Text + "' and Password = '" + textBox2.Text + "'  and Permissions =  2", con);
            DataTable dt2 = new DataTable();
            sda2.Fill(dt2);

            //Faculty Login
            SqlDataAdapter sda3 = new SqlDataAdapter("Select Count(*) From Login Where Username = '" + textBox1.Text + "' and Password = '" + textBox2.Text + "'  and Permissions =  3", con);
            DataTable dt3 = new DataTable();
            sda3.Fill(dt3);

            //Admin Login Success
            if (dt.Rows[0][0].ToString() == "1")
            {
                this.Hide();
                Welcome_Window ww = new Welcome_Window();

                ww.Show();
            }

            //Janitor Login Success
            else if (dt2.Rows[0][0].ToString() == "1")
            {
                this.Hide();
                JMTicketViewer jea = new JMTicketViewer();
//                EmergencyNotice en = new EmergencyNotice();
               
                jea.Show();
//                en.Show();
            }

            //Faculty Login Success
            else if (dt3.Rows[0][0].ToString() == "1")
            {
                this.Hide();
                EmergencyRequest er = new EmergencyRequest();

                er.Show();
            }

            //Login Failure
            else
                MessageBox.Show("Please check your Username or Password");   
        }
    }
}






//Code for window 2/ Welcome Window
namespace Finalproject
{
    public partial class Welcome_Window : Form
    {
        
        public Welcome_Window()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {            
            AddRemoveEmployee are = new AddRemoveEmployee();
            are.Show();               
        }

        private void JanitorialEquipmentAssignment_Click(object sender, EventArgs e)
        {            
            JMAssign jma = new JMAssign();
            jma.Show();
        }

        private void Search_Click(object sender, EventArgs e)
        {           
            Search de = new Search();
            de.Show();
        }

        private void AddRoom_Click(object sender, EventArgs e)
        {            
            AddRemoveRoom ar = new AddRemoveRoom();
            ar.Show();
        }

        private void button5_Click(object sender, EventArgs e)
        {            
            AddRemoveEquipment ei = new AddRemoveEquipment();
            ei.Show();
        }

        private void addRemoveEmployeeToolStripMenuItem_Click(object sender, EventArgs e)
        {            
            AddRemoveEmployee are = new AddRemoveEmployee();
            are.Show();
        }

        private void EmergencyInput_Click(object sender, EventArgs e)
        {
            EmergencyReq emer = new EmergencyReq();
            emer.Show();
        }

        private void AddRoomSchedule_Click(object sender, EventArgs e)
        {
            AddRemoveRoomSchedule rs = new AddRemoveRoomSchedule();
            rs.Show();
        }

        private void CloseButton_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
}

//Code for window 3/ Search Window

namespace Finalproject
{
    public partial class Search : Form
    {
        public Search()
        {
            InitializeComponent();
        }

        private void SearchButton_Click(object sender, EventArgs e)
        {
            if (EmpRadio.Checked)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM AddEmp", con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }
            
            if (AssignmentRadio.Checked)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM JMTickets", con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }
            

            if (RoomRadio.Checked)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM AddRoom", con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }

            if (RoomScheduleRadio.Checked)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM RoomSched", con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }

            if (EquipmentRadio.Checked)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM EquipmentInput", con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }
        }

        private void CloseButton_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void PrintButton_Click(object sender, EventArgs e)
        {
            MessageBox.Show("View Printed!!");
        }
    }
}



//Code window 4/ 
namespace Finalproject
{
    public partial class JMTicketViewer : Form
    {
        public JMTicketViewer()
        {
            InitializeComponent();
        }

        private void SearchButton_Click(object sender, EventArgs e)
        {
            int number;
            bool result = Int32.TryParse(EmpIDTextBox.Text, out number);

            if (result)
            {
                SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
                con.Open();
                SqlDataAdapter sda = new SqlDataAdapter("SELECT [Ticket ID], Emergency, Description, [Room Number], Date FROM JMTickets WHERE [Assigned Employee] = " + Convert.ToInt32(EmpIDTextBox.Text), con);
                DataTable data = new DataTable();
                sda.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
            }

            else
                MessageBox.Show("Please enter your ID");
        }
    }
}


//Code for window 4
namespace Finalproject
{
    public partial class JMAssign : Form
    {
        public JMAssign()
        {
            InitializeComponent();
        }

        private void AddButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO JMTickets ([Room Number],Description,Emergency,Date,Assignment,[Assigned Employee],[Time Start], [Time End]) VALUES ('" + 
                                                    RoomNumTextBox.Text + "','" + DescriptionTextBox.Text + "','" + "No','" + DateTextBox.Text + "','" + 
                                                    AssignmentComboBox.Text + "','"  + EmpIDTextBox.Text + "','" + TimeStartTextBox.Text + "','" + 
                                                    TimeEndTextBox.Text + "')", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Assignment added!!"); 
        }

        private void RemoveButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM JMTickets WHERE [Ticket ID]= '" + TicketIDTextBox.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Assignment deleted!!"); 
        }
    }
}



//code for window 5

namespace Finalproject
{
    public partial class EmergencyRequest : Form
    {
        public EmergencyRequest()
        {
            InitializeComponent();
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();

    
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO EmergencyReq ([ROOMNO],[CLEREP],[CLEREPDESCRIP],[EQUIPID]) VALUES ('" + textBox2.Text + "','" + textBox3.Text + "','" + textBox4.Text + "','" + textBox5.Text + "')", con);
            sda.SelectCommand.ExecuteNonQuery(); // <--************ NOTE: to add data in table, remove comment "//" , or add "//" to stop table data entry ***************
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();


            MessageBox.Show("Room #:         " + textBox2.Text + "\n" + "Cleanup/Repair: " + textBox3.Text + "\n" + "Description:        " + textBox4.Text + "\n" + "Equip ID:       " + textBox5.Text, "Emergency Request Added!!");



//            EmergencyNotice en = new EmergencyNotice();
//            en.Show();
            

        }

        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM EmergencyReq WHERE [MainTicket] = '" + textBox1.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();
            MessageBox.Show("Request deleted!!");
        }

        private void checkBox1_CheckedChanged(object sender, EventArgs e)
        {
            if (checkBox1.Checked)
            {
                textBox3.Text = "Repair";
            }
            else
            {
                textBox3.Text = "Cleanup";
            }
        }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }


        private void dataGridView1_MouseClick(object sender, MouseEventArgs e)
        {
            textBox1.Text = dataGridView1.SelectedRows[0].Cells[0].Value.ToString();
        }
    

    }
}




//Code for window 6

namespace Finalproject
{
    public partial class EmergencyReq : Form
    {
        public EmergencyReq()
        {
            InitializeComponent();
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO EmergencyReq ([Room Number],[Cleanup or Repair],[Description],[Equipment ID]) VALUES ('" + textBox2.Text + "','" + textBox3.Text + "','" + textBox4.Text + "','" + textBox5.Text + "')", con);
            sda.SelectCommand.ExecuteNonQuery();
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();
            MessageBox.Show("Emergency Request added!!"); 

        }

        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM EmergencyReq WHERE [ID] = '" + textBox1.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM EmergencyReq", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();
            MessageBox.Show("Request deleted!!"); 

        }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }

        private void dataGridView1_MouseClick(object sender, MouseEventArgs e)
        {
            textBox1.Text = dataGridView1.SelectedRows[0].Cells[0].Value.ToString();
            //textBox2.Text = dataGridView1.SelectedRows[0].Cells[1].Value.ToString();
            //textBox3.Text = dataGridView1.SelectedRows[0].Cells[2].Value.ToString();
            //textBox4.Text = dataGridView1.SelectedRows[0].Cells[2].Value.ToString();

        }

        private void EmergencyReq_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the 'lOGINDataSet7.EmergencyReq' table. You can move, or remove it, as needed.
            //this.emergencyReqTableAdapter1.Fill(this.lOGINDataSet7.EmergencyReq);
            // TODO: This line of code loads data into the 'lOGINDataSet1.EmergencyReq' table. You can move, or remove it, as needed.
            //this.emergencyReqTableAdapter.Fill(this.lOGINDataSet1.EmergencyReq);

        }

        private void checkBox1_CheckedChanged(object sender, EventArgs e)
        {
            if (checkBox1.Checked)
            {
                textBox3.Text = "Repair";
            }
            else
            {
                textBox3.Text = "Cleanup";
            }
        }
    }
}




//Code for window 6


namespace Finalproject
{
    public partial class AddRemoveRoomSchedule : Form
    {
        public AddRemoveRoomSchedule()
        {
            InitializeComponent();
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM RoomSched", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
        }
        
        private void AddButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();

            
                SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO [RoomSched] (Room, Date, [Time Start], [Time End], Description) VALUES ('" + RoomTextBox.Text + "','" + dateTimePicker1.Value.Date + "','" + dateTimePicker2.Value.TimeOfDay + "','" + dateTimePicker3.Value.TimeOfDay + "','" + DescriptionTextBox.Text + "')", con);
                       
                sda.SelectCommand.ExecuteNonQuery();
                SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM RoomSched", con);

                DataTable data = new DataTable();
                sda1.Fill(data);

                
                if (data.Rows[0][0].ToString() == "1")
                {
                    this.Hide();
                    Welcome_Window ww = new Welcome_Window();

                    ww.Show();
                }

                dataGridView1.DataSource = data;
                con.Close();
                MessageBox.Show("Room schedule added!!");
           
            
                //MessageBox.Show("You already added a schedule with this information");
            
        }

        private void RemoveButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM RoomSched WHERE [ID] = '" + textBox6.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM RoomSched", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();
            MessageBox.Show("Room schedule deleted!!"); 
        }

        private void ViewButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM RoomSched", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
        }

        private void AddRemoveRoomSchedule_Load(object sender, EventArgs e)
        {

        }

        private void dataGridView1_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {

        }

        private void dataGridView1_MouseClick(object sender, MouseEventArgs e)
        {
            textBox6.Text = dataGridView1.SelectedRows[0].Cells[0].Value.ToString();
        }        
    }
}

//code for window 8

namespace Finalproject
{
    public partial class AddRemoveRoom : Form
    {
        public AddRemoveRoom()
        {
            InitializeComponent();
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM AddRoom", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO AddRoom ([Room Number],Description,Location,[Employee Access ID]) VALUES ('" + textBox1.Text + "','" + textBox2.Text + "','" + textBox3.Text + "','" + textBox4.Text + "')", con);
            try
            {
                sda.SelectCommand.ExecuteNonQuery();
                SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM AddRoom", con);
                DataTable data = new DataTable();
                sda1.Fill(data);
                dataGridView1.DataSource = data;
                con.Close();
                MessageBox.Show("Room added!!");
            }
            catch (Exception ex)
            {                
                MessageBox.Show("You already added this room number");
            }
            
             
        }

        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM AddRoom WHERE [Room Number] = '" + textBox1.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            SqlDataAdapter sda1 = new SqlDataAdapter("SELECT * FROM AddRoom", con);
            DataTable data = new DataTable();
            sda1.Fill(data);
            dataGridView1.DataSource = data;
            con.Close();
            MessageBox.Show("Room deleted!!"); 
        }

        private void button3_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open(); 
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM AddRoom", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
            
        }

        private void dataGridView1_MouseClick(object sender, MouseEventArgs e)
        {
            textBox1.Text = dataGridView1.SelectedRows[0].Cells[0].Value.ToString();
            textBox2.Text = dataGridView1.SelectedRows[0].Cells[1].Value.ToString();
            textBox3.Text = dataGridView1.SelectedRows[0].Cells[2].Value.ToString();
            textBox3.Text = dataGridView1.SelectedRows[0].Cells[2].Value.ToString();
        }

    }
}


//code for window 9


namespace Finalproject
{
    public partial class AddRemoveEquipment : Form
    {
        public AddRemoveEquipment()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO EquipmentInput ([Room Number],[Equipment ID],Manufacturer,[Equipment Description],Status) VALUES ('" + textBox1.Text + "','" + textBox2.Text + "','" + textBox3.Text + "','" + comboBox1.Text + "','" + comboBox2.Text + "')", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Equipment Added!!!");
        }

        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM EquipmentInput WHERE [Equipment ID] = '" + textBox2.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Equipment Removed!!!");
        }

        private void button3_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("SELECT * FROM EquipmentInput", con);
            DataTable data = new DataTable();
            sda.Fill(data);
            dataGridView1.DataSource = data;
            con.Close(); 
        }
    }
}



//code for window 10

namespace Finalproject
{
    public partial class AddRemoveEmployee : Form
    {
        public AddRemoveEmployee()
        {
            InitializeComponent();
        }

        private void AddButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("INSERT INTO AddEmp([First Name],[Last Name],MavID,Pin,Position,Email) VALUES ('" + FNameTextBox.Text + "','" + LNameTextBox.Text + "','" + MavIDTextBox.Text + "','" + PinTextBox.Text + "','" + PositionTextBox.Text + "','" + EmailTextBox.Text + "')", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Employee added!!");
        }

        private void RemoveButton_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection(@"Data Source=(LocalDB)\v11.0;AttachDbFilename=C:\Projects\Latest_Finalproject\Finalproject\LOGIN.mdf;Integrated Security=True;Connect Timeout=30;");
            con.Open();
            SqlDataAdapter sda = new SqlDataAdapter("DELETE FROM AddEmp WHERE MavID = '" + MavIDTextBox.Text + "'", con);
            sda.SelectCommand.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Employee removed!!");
        }
    }
}









