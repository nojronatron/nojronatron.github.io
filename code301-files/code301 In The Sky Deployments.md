# In The Sky Deployments

## Heroku

Simon owns BE in the cloud
JOTFORM_API='simons key for now'
JOTFORM_TEMPLATE=
JWKS_URI=<auth0_well_known\jwks.json_belongs_to_Simon>
MONGO_DB=<Jons_survery_surveyors_project>

## Netlify

Allen owns FE in the cloud
REACT_APP_SERVER_URL="https://working-301-final.herokuapp.com"
REACT_APP_AUTH_DOMAIN="" <from simons account>
REACT_APP_AUTH_CLIENT_ID="" <from simons account>
REACT_APP_AUTH_REDIRECT_URL="" <the netlify front-end URL>


## Jon Local Deployment

FE
REACT_APP_SERVER_URL=http://localhost:3001
REACT_APP_AUTH_DOMAIN=dev-mgtjufdj.us.auth0.com
REACT_APP_AUTH_CLIENT_ID=XGi5wGmMnn3e6avlZFHyXlwbDckt4OjX
REACT_APP_AUTH_REDIRECT_URI=http://localhost:3000



this.props.isAuthenticated, user?: true {given_name: 'Jon', family_name: 'Rumsey', nickname: 'jon.rumsey', name: 'Jon Rumsey', picture: 'https://lh3.googleusercontent.com/a-/AOh14GiXhvqzMMIIpbY_tMVm9KnKj1rTKiDCtbj3DtLjUA=s96-c', …}
Admin.js:31 we are looking at Admin.js true
(index):328 Uncaught DOMException: Failed to execute 'replaceState' on 'History': A history state object with URL 'https://www.jotform.com/' cannot be created in a document with origin 'https://submit.jotform.com' and URL 'https://submit.jotform.com/submit/221227475582054/'.
    at https://submit.jotform.com/submit/221227475582054/:328:22

