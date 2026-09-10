## What is DOTNET.

- .NET is a runtime that C# programs are built with and run on.
- C# programs are run on a virtual execution system called the Common Language Runtime(CLR), and set of class libraries.
- .NET supports other languages(Visual Basic, F#, etc) and allows the write other programming languages in one application.
- One runtime that allows you to build games, web, desktop, mobile and several other solutions
- Cross-platform(for most application types)

## What is ASP.NET Core?

- ASP.NET Core is the modern, high-performance web development framework for .NET.
- It is a Open source on GitHub with over 100000 contributions.
- Its platform independent i.e. runs on Windows, Linux, macOS and Docker.
- A re-design of earlier Windows-only version of ASP.NET
- Stable ad mature, and you can create great web applications.
- Supports industry standard several development patterns:
	Razor Pages(MVVM), MVC, Blazor Server
- Razor Pages - This project type implements the Model=> view - View=> Model pattern where C# is written in a class file, directly attached to the frontend file.


## What is an API ?
- API stands for Application Programming Interface
- It allows different software applications to communicate
- APIs define how request and response should be structured
- Examples: 
	- Web API's
	- Operating system API;s
	- Library API's


## Types of APIs
- Web APIs(REST. SOAP, GraphQL)
- Library API's(used within programming languages)
- Operating System APIs (e.g.  DirectX for graphics processing)


## Code Snippet
---------------

```csharp
using HotelListing.API.Data;
using Microsoft.AspNetCore.Mvc;

// For more information on enabling Web API for empty projects, visit https://go.microsoft.com/fwlink/?LinkID=397860

namespace HotelListing.API.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class HotelsController : ControllerBase
    {

        private static List<Hotel> hotels = new List<Hotel>
        {
            new Hotel {Id= 1, Name= "Jagannath", Address="Bangalore", Rating = 4.5},
            new Hotel {Id= 2, Name= "Jagannath", Address="Mumbai", Rating = 4.8},
        };


        // GET: api/<HotelsController>
        //[HttpGet]
        //public IEnumerable<string> Get()
        //{
        //    return new string[] { "value1", "value2" };
        //}

        // GET: api/<HotelsController>
        [HttpGet]
        public ActionResult<IEnumerable<Hotel>> Get()
        {
            return Ok(hotels);
        }


        // GET api/<HotelsController>/5
        [HttpGet("{id}")]
        public ActionResult<Hotel> Get(int id)
        {
            var hotel = hotels.FirstOrDefault(h => h.Id == id);
            if (hotel == null)
            {
                return NotFound();
            }
            return Ok(hotel);
        }

        // POST api/<HotelsController>
        [HttpPost]
        public ActionResult<Hotel> Post([FromBody] Hotel newHotel)
        {
            if (hotels.Any(h => h.Id == newHotel.Id))
            {
                return BadRequest("Hotel with this id is already exists");
            }
            hotels.Add(newHotel);
            return CreatedAtAction(nameof(Get), new { id = newHotel.Id }, newHotel);

        }

        // PUT api/<HotelsController>/5
        [HttpPut("{id}")]
        public ActionResult Put(int id, [FromBody] Hotel updateHotel)
        {
            var existingHotel = hotels.FirstOrDefault(h => h.Id == id);
            if (existingHotel == null)
            {
                return NotFound();
            }

            existingHotel.Name = updateHotel.Name;
            existingHotel.Address = updateHotel.Address;
            existingHotel.Rating = updateHotel.Rating;
            return NoContent();
        }

        // DELETE api/<HotelsController>/5
        [HttpDelete("{id}")]
        public ActionResult Delete(int id)
        {
            var hotel = hotels.FirstOrDefault(h => h.Id == id);
            if (hotel == null)
            {
                return NotFound(new { message = "Hotel not found" });
            }

            hotels.Remove(hotel);
            return NoContent();
        }
    }
}

```

## Explanation of each keywords and classes used above.

-- HotelsController exposes REST API endpoints for managing hotels.


This is called CRUD:

- Create → POST - Used to create record/records
- Read → GET - Used to Get one/many record/records
- Update → PUT  - Used to update the record
- Delete → DELETE - Used to delete the record

## using -- statements

using HotelListing.API.Data;
using Microsoft.AspNetCore.Mvc;

using allows you to use classes from a namespace without writing the complete namespace every time.

A using directive allows us to access types from a namespace without specifying the fully qualified namespace name every time. It also improves readability.


## ControllerBase

public class HotelsController : ControllerBase

ControllerBase is provided by ASP.NET Core and gives your API controller useful functionality.

Ok()
NotFound()
BadRequest()
NoContent()
CreatedAtAction()

## ApiController

This is an attribute.

Attributes provide metadata/configuration about classes, methods, properties, etc.

Note: [ApiController] marks a class as an API controller and enables API-specific behaviors such as automatic model validation, improved parameter binding, and automatic 400 responses when model validation fails.

## [Route("api/[controller]")]

This defines the base URL for your controller.

Your controller is: => HotelsController =>ASP.NET Core replaces: => [controller] => Hotels

final URL will be

/api/hotels

HotelsController => once the url builds the Controller keyword is removed as its a naming convention 

- HttpGet => This method handles HTTP GET requests.
- 


## ActionResult

ActionResult<IEnumerable<Hotel>>

ActionResult represents the HTTP response returned by your controller.


## IEnumerable<Hotel>

You could return List<Hotel>, but IEnumerable<Hotel> exposes only the behavior needed to enumerate the collection and keeps the return type more abstract.


##  Static list

means the variable belongs to the class itself, rather than an individual object/instance.

Because the list is static, all instances of HotelsController share the same list.


1. What is ASP.NET Core Web API?
ASP.NET Core Web API is a framework for building HTTP-based APIs that can be consumed by applications such as web applications, mobile apps, desktop applications, or other services.

2. What is a controller?
A controller handles incoming HTTP requests, performs the required application logic or delegates it to services, and returns an HTTP response.

3. What is ControllerBase?
ControllerBase is the base class commonly used for ASP.NET Core Web API controllers. It provides methods such as Ok(), NotFound(), BadRequest(), and NoContent().

4. What is [ApiController]?
It marks a class as an API controller and enables API-specific behaviors such as automatic model validation and improved parameter binding.

5. What is routing?
Routing maps an incoming HTTP request to the appropriate controller/action.

6. What is [HttpGet]?
It indicates that a controller action handles HTTP GET requests.


















