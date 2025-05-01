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

namespace MySqlProject
{
    public partial class LoginForm : Form
    {
        public LoginForm()
        {
            InitializeComponent();
        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }


        void insertupdatedelete(String query) // This fucntion work for insert, update and delete data from sql database just pass query in this function

        {
            //1. Address of sql server and database
            String constring = "Data Source=DESKTOP-0I305DL\\SQLEXPRESS;Initial Catalog=firstproject;Integrated Security=True";
            //2. Establish Connection
            SqlConnection con = new SqlConnection(constring);
            //3. Open Connection
            con.Open();
            //5. execute qurey
            SqlCommand cmd = new SqlCommand(query, con);
            cmd.ExecuteNonQuery();
            //Close Connection

            con.Close();
        }
       public DataTable selectdata(string query)// this function used to select data from database

        {
            DataTable datatable = new DataTable();
            //1. Address of sql server and database
            String constring = "Data Source=DESKTOP-0I305DL\\SQLEXPRESS;Initial Catalog=firstproject;Integrated Security=True";
            // String s = "DESKTOP-0I305DL\\SQLEXPRESS;Initial Catalog=firstproject;Integrated Security=True";
            //2. Establish Connection
            SqlConnection con = new SqlConnection(constring);
            //3. Open Connection
            con.Open()
            //5. execute qurey
            SqlCommand cmd = new SqlCommand(query,con);
            SqlDataAdapter sda = new SqlDataAdapter(cmd);
           sda.Fill(datatable);
            con.Close();
            return datatable;
            
        }
        private void btnSave_Click(object sender, EventArgs e)//qurey pass against btnSave and call insertuppdatedelete fucntion
        {
            //4. Prepare Query
        String query = " insert into Name(FirstName,LastName)values('"+txtFirstName.Text+"','"+txtLastName.Text+"')";

            insertupdatedelete(query);
            MessageBox.Show("Data saved");
        }

        private void btnShowData_Click(object sender, EventArgs e)
        {
            dataGridView1.Rows.Clear();
            String query = "select * from name";
            DataTable dt = new DataTable();
          dt = selectdata(query);
            dataGridView1.DataSource = dt;
       
        }

        private void btnUpdate_Click(object sender, EventArgs e)//qurey pass against btnUpdate and call insertuppdatedelete fucntion
        {
            String query = "update Name set firstname = '"+txtFirstName.Text+"' , lastname = '"+txtLastName.Text+"' where id = "+txtId.Text+"";
           insertupdatedelete(query);
        }

        private void btnDelete_Click(object sender, EventArgs e)//qurey pass against btnDelete and call insertuppdatedelete fucntion
        {
            String query = "	delete from name where id = "+txtId.Text+"";
            insertupdatedelete(query);
            MessageBox.Show("Deleted Sucessfully");
        }
    }
}
