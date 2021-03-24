# Test Lesson

## Info

This is a test lesson you can use to practice the `github-to-canvas` gem.

## Setting Up GitHub Actions Workflow

In GitHub, it is possible to use the `github-to-canvas` gem in combination with GitHub Actions to automatically sync a repository README.md file with a Canvas lesson.

The following steps are required for getting this set up:

- Navigate to the course in Canvas that you'd like to set up.

- Create a page or assignment in Canvas. This can be a blank lesson to start. If you already have a lesson in mind, navigate to that lesson, instead

- Note the URL of the lesson. It has a few pieces of info we'll need in a moment. For example, this URL is from an existing lesson:

  ```txt
  https://learning.flatironschool.com/courses/4056/pages/test-lesson-for-gem?module_item_id=192408
  ```

  The URL contains the course ID, `4056` in the example above, the type of lesson, `page` in this case, and the lesson name, `test-lesson-for-gem`. 

- Go to the GitHub repository you'd like to connect to the lesson. 

- Add an Actions workflow to the repository. This can be done in a few ways:
  - Click the **Actions** tab and scroll down. A few actions have already been created for learn-co-curriculum that you can use, one default. The default workflow is called **Canvas Sync Workflow**. Click this one and it'll create a file, `canvas-sync.yml` inside a new `./.github/workflows` directory on your repo. Click **Start commit** on the right and choose to commit the new file.
  - Alternatively, you can create the file manually by copy/pasting from an existing workflow. [This lesson](https://github.com/learn-co-curriculum/phase-0-flatiron-school-philosophy), for example, has a pre-work workflow set up. Once there is a `/.github/workflows/some-name.yml` file present, the workflow will automatically be enabled.

- Add a `.canvas` file to the repo. The file should look like this:

  ```
  ---
  :lessons:
  - :id: welcome
    :course_id: 3280
    :canvas_url: https://learning.flatironschool.com/courses/3280/pages/welcome-to-flatiron-school
    :type: page
  ```
  
  Replace the values in the file with info from your Canvas lesson - the `id` will be the value/text after `/pages/` or `/assignments/` in the URL (but before `?` if present). It could be a slugified title like `test-lesson-for-gem` or a number like `12313`. Change the course ID and lesson type accordingly and copy paste the lesson URL to `:canvas_url:`. 
  
- With the workflow set up and the `.canvas` file created, make an edit to the `README.md` file and commit it. Then click on the **Actions** tab again. You should be able to watch the GitHub Action work through the process there. When finished, go to the lesson in Canvas

## Troubleshooting

The `github-to-canvas` gem names Canvas lessons based on the top-level header inside the `README.md` file (i.e. `# Test Lesson`). If you are updating an existing lesson, it may be good to align the lesson title with the GitHub `README.md` header. If you are updating a Canvas page, make sure `.canvas` has an id that matches the sluggified Canvas title. If the lesson and `README.md` titles are not the same, the lesson in Canvas will be given a new slugified title, which may not match what is in the `.canvas` file (and will cause issues for future workflows).

