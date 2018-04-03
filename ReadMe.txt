Database First Approach (Web API + SQL Server )
================================================================
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Web.Http;
using EmployeeDataAccess;

namespace EmployeeService.Controllers
{
    public class EmployeesController : ApiController
    {
        public IEnumerable<Employee> Get()
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                return entities.Employees.ToList();
            }
        }

        public Employee Get(int id)
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                return entities.Employees.FirstOrDefault(e => e.ID == id);
            }
        }

        public void Post([FromBody] Employee employee)
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                entities.Employees.Add(employee);
                entities.SaveChanges();
            }
        }

        public void Delete(int id)
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                entities.Employees.Remove(entities.Employees.FirstOrDefault(e => e.ID == id));
                entities.SaveChanges();
            }
        }

        public void Put(int id, [FromBody]Employee employee)
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                var entity = entities.Employees.FirstOrDefault(e => e.ID == id);

                entity.FirstName = employee.FirstName;
                entity.LastName = employee.LastName;
                entity.Gender = employee.Gender;
                entity.Salary = employee.Salary;

                entities.SaveChanges();
            }
        }
    }
}
===================================================================


http://csharp-video-tutorials.blogspot.in/2016/09/aspnet-web-api-and-sql-server.html

https://www.youtube.com/results?search_query=web+api+with+sql+server+database

http://csharp-video-tutorials.blogspot.in/2016/09/aspnet-web-api-tutorial-for-beginners.html