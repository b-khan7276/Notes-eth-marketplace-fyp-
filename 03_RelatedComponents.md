# RelatedComponents

  ## Data:
  
  - Create new folder for content
  - I created folder named `courses` and a file name inside that folder `feter.js`
  - I create a file `index.json` and store static data in json formate
  ## Calling the static data 
  -  I Created a static funtion call *getAllCourse* 
  -  and call the data from the  data like this
   ```javascript
    export function getStaticProps() {
  const { data } = getAllCourses()
  return {
    props: {
      courses: data
    }
  }
}
```
  - And I call the data in home function like this
  ```Javascript
  export default function Home({courses}) {
  return (
    <>
      <Hero />
      <CourseList
        courses={courses}
      />
    </>
  )
}
```
## Passing the props 
- Then I pass the props
- as Courses
- I call the props in a file `components/courses/list/index.js`
- I call the props in List function like this
`` typescript
export default function List({courses}) {
  return (
    <section className="grid grid-cols-2 gap-4 mb-5">
      { courses.map(course =>
        <div
          key={course.id}
          ```
- Then I pass the values of `courses data` into tags

## optimizing Images in
- I optimize imges in  `list/index.js`
- I used the nextjs image tag in my file 
- And used it insted of <img> tag like so
```javascript
     <Image
                className="object-cover"
                src={course.coverImage}
                layout="fixed"
                width="200"
                height="230"
                alt={course.title}/>
 ```
 # Course Detail page
 - I made a folder Name `Corses` in a `pages` folder 
 - I made a file by the name of `[slug].js`
 - Now I copy the code of `courses.js` into `[slug].js` 
  ```js
  export default function Course() {

 
  
    return (
   <>
   <div className="py-4">
       <CourseHero/>
       </div>
        <Keypoints/>
       <Curriculum/>
       <Modal/>
       </>
    )
  }

  Course.Layout = BaseLayout
  ```
  - Then I edit the `course/list/index`
  - and Add *Link* tag into it 
  ```js
    <Link  href={`/courses/${course.slug}`}>
              <a
               
                className="block mt-1 text-lg leading-tight font-medium text-black hover:underline">
                {course.title}
              </a>
              </Link>
 ```
 - then I edit `Navbar/index.js` 
 - and Added Link tag to it 
 - Like so 
 ```js 
 <div>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Home
                </a>
              </Link>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Marketplace
                </a>
              </Link>
              <Link href="/" >
                <a
                  className="font-medium mr-8 text-gray-500 hover:text-gray-900">
                  Blogs
                </a>
              </Link>
            </div>
```
   
## Custamize data for each course
- I write a function to get a single course by slug 
- in a file `[slug].js`
- the function is 
```js
//  To get the static paths 
export function getStaticPaths(){
    //  Fetch all our courses
    const {data} = getAllCourses()
    //  Now many pages you want to return 
    return{
        paths: data.map(c =>({
            params:{
                slug: c.slug
            }
        })), fallback:false

    }
}
```
- I will also need static props so
- I will write a function for get staticprops
- and i will call a single course by *params.slug*
```js//  Adding the props also 
export function getStaticProps({params}) {
    const { data } = getAllCourses()
    //  Search for single course
    const course = data.filter(c => c.slug === params.slug)[0]
    return {
      props: {
        course
      }
    }
  ```
  

