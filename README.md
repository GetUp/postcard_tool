# postcard_tool
script to send postcards through the ScribblePics API

## requirements

You need the "rest-client" gem: `gem install rest-client`

Set or provide two environment variables:

    SCRIBBLEPICS_API_KEY
    SCRIBBLEPICS_API_URL

## Usage

The tool requires a recipient (see recipient.yml for example details), messages to send (see query_result.csv) and an image for the front of the postcard.  The back of the card can only be changed by ScribblePics.

The default mode is to produce a list of preview URLs.  Add `-s` or `--send-cards` to actually send the cards.

### Providing the image

You can upload front images independently:

    ./postcard_tool -u postcard_front.jpg

Or during the preview/send:

    ./postcard_tool -f query_result.csv -r recipient.yml -u postcard_front.jpg

You can also link to a web-based image:

    ./postcard_tool -f query_result.csv -r recipient.yml -l "http://example.com/postcard_front.jpg"

Or use a previously uploaded image:

    ./postcard_tool -f query_result.csv -r recipient.yml -i "c9234ec7-ed7b-4dc4-ac79-abcdefgh"

## Process
1. Export CSV from sequel pro the messages you want.  Use a query like `SELECT id, body FROM user_emails WHERE page_id = 2000 AND id NOT IN (<already sent IDs>)`
2. Scrub the CSV for: test postcards, postcards that are templates only, obscenities
3. Try a dry run of the script. Eyeball the output postcards for length (some might get cut off) or template text
4. If all goes well, send the postcards by using the -s flag.
