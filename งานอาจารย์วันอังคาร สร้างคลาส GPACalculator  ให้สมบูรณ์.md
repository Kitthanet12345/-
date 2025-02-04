namespace WinFormsApp6
{
    public partial class Form1 : Form

     using System;
     using System.Linq;
     using System.Windows.Forms;

     namespace GradeCalculator
    {
        public Form1()
        {
           InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string[] gradeStrings = txtGrades.Text.Split(',');
            double[] grades;
            try
            {
                grades = Array.ConvertAll(gradeStrings, double.Parse);
            }
            catch
            {
                MessageBox.Show("????????????????????????????? (???? 85,90,78)");
                return;
            }

            if (grades.Length == 0)
            {
                MessageBox.Show("???????????????");
                return;
            }

            double gpa = grades.Average();
            double maxGrade = grades.Max();
            double minGrade = grades.Min();
            int numStudents = grades.Length;

            lblResult.Text = $"GPA: {gpa:F2}\n" +
                             $"???????: {numStudents}\n" +
                             $"???????????: {maxGrade}\n" +
                             $"???????????: {minGrade}";
        }
    }
}
