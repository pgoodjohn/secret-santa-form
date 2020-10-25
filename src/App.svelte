<script>
  import axios from "axios";
  import Swal from "sweetalert2";
  const year = new Date();
  let name = '';
  let email = '';

  function handleSubmit(event) {
    let participant = {
      name: name,
      email: email
    };

    let data = {
      data: participant
    };

    let url = `https://europe-west1-personal-projects-239316.cloudfunctions.net/secret-santa-api`;
    // let url = `http://localhost:8000/`;

    axios
      .post(url, data)
      .then(function(response) {
        Swal.fire({
          title: "Success!",
          text: "Thank you!",
          icon: "success",
          confirmButtonText: "Cool"
        });
        name = '';
        email = '';
      })
      .catch(function(error) {
	console.log(error)
        Swal.fire({
          title: "Error!",
          text: "Unable to save",
          icon: "error",
          confirmButtonText: "Sad"
        });
      });
  }
</script>

<main>
  <div class="container mx-auto p-8">
    <h1>I Cagnacci #SecretSanta {year.getFullYear()}</h1>

    <div class="flex justify-center p-4">
      <img
        alt="Santa Claus"
        src="https://res.cloudinary.com/pgoodjohn/image/upload/v1603565334/SecretSantaForm/santa.jpg"
        width="150px" />
    </div>

    <form on:submit|preventDefault={handleSubmit}>
      <input
        class="bg-white focus:outline-none focus:shadow-outline border
        border-gray-300 rounded-lg py-2 px-4 block w-full appearance-none
        leading-normal"
        bind:value={name}
        id="name"
        placeholder="Nome"
        />
      <br />
      <input
        class="bg-white focus:outline-none focus:shadow-outline border
        border-gray-300 rounded-lg py-2 px-4 block w-full appearance-none
        leading-normal"
        bind:value={email}
        id="email"
        type="email"
        placeholder="Email"
        />
      <br />
      <button
        class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold
        hover:text-white py-2 px-4 border border-blue-500
        hover:border-transparent rounded"
        disabled={(name === '' && email === '')}>
        Conferma
      </button>
    </form>
  </div>
</main>
