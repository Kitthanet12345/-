namespace WinFormsApp7
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void txtName_Click(object sender, EventArgs e)
        {

        }

        private void txtStudentID_TextChanged(object sender, EventArgs e)
        {
            using System;
            using System.Collections.Generic;


class Student
        {
            public string StudentID { get; set; }
            public string Name { get; set; }
            public string Major { get; set; }
            public Advisor Advisor { get; set; } 

            public Student(string studentID, string name, string major)
            {
                StudentID = studentID;
                Name = name;
                Major = major;
                Advisor = null;  
            }

            public void SetAdvisor(Advisor advisor)
            {
                Advisor = advisor;
            }

            public override string ToString()
            {
                return $"{StudentID}: {Name}, {Major}";
            }
        }

      
        class Advisor
        {
            public string Name { get; set; }
            public string Major { get; set; }
            public List<Student> Students { get; private set; } 

            public Advisor(string name, string major)
            {
                Name = name;
                Major = major;
                Students = new List<Student>();
            }

            public void AddStudent(Student student)
            {
                if (student.Advisor == null) 
                {
                    student.SetAdvisor(this);
                    Students.Add(student);
                }
                else
                {
                    Console.WriteLine($"StudenthaveTeacher: {student.Name}");
                }
            }

            public void ShowStudents()
            {
                Console.WriteLine($"StudentsTeacher {Name} :");
                foreach (var student in Students)
                {
                    Console.WriteLine($"- {student.Name} ({student.StudentID})");
                }
            }

            public Student GetTopStudent()
            {
              
                return Students.Count > 0 ? Students[0] : null;  
            }
        }

        class StudentManagement
        {
            private List<Student> students = new List<Student>();
            private List<Advisor> advisors = new List<Advisor>();

            public void AddStudent(Student student)
            {
                students.Add(student);
            }

            public void AddAdvisor(Advisor advisor)
            {
                advisors.Add(advisor);
            }

            public void ShowAllStudents()
            {
                Console.WriteLine("Allstudent:");
                foreach (var student in students)
                {
                    Console.WriteLine(student);
                }
            }

            public void ShowAdvisorStudents(string advisorName)
            {
                foreach (var advisor in advisors)
                {
                    if (advisor.Name == advisorName)
                    {
                        advisor.ShowStudents();
                        return;
                    }
                }
                Console.WriteLine($"NotfoundTeacher {advisorName}");
            }

            public void ShowTopStudent()
            {
                Student topStudent = null;
                foreach (var student in students)
                {
                    
                    if (topStudent == null || int.Parse(student.StudentID.Substring(1)) > int.Parse(topStudent.StudentID.Substring(1)))
                    {
                        topStudent = student;
                    }
                }
                if (topStudent != null)
                {
                    Console.WriteLine($"StudentTopScore: {topStudent.Name}, score: {topStudent.StudentID}");
                }
                else
                {
                    Console.WriteLine("NotStudentTopScore");
                }
            }
        }

      
        class Program
        {
            static void Main(string[] args)
            {
          
                Student student1 = new Student("673450392-2", "Suwit", "Cs");
                Student student2 = new Student("673450392-8", "Suwana", "CS");

                Advisor advisor1 = new Advisor("TeacherSomtum", "Cs");

                StudentManagement management = new StudentManagement();

                
                management.AddAdvisor(advisor1);
                management.AddStudent(student1);
                management.AddStudent(student2);

            
                advisor1.AddStudent(student1);
                advisor1.AddStudent(student2);

                management.ShowAllStudents();

                management.ShowAdvisorStudents("TeacherSomtum");

                management.ShowTopStudent();
            }
        }

    }
}
}
