# httpExemplo
projetos criados


try {
         
        URL url = new URL("https://www.googleapis.com/youtube/v3/playlistItems?part=snippet"
                + "&key="+key
                + "&access_token=" + access_token);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setDoOutput(true);
        conn.setRequestMethod("POST");
        conn.setRequestProperty("Content-Type", "application/json");
 
        String input = "{ \"snippet\": {\"playlistId\": \"WL\",\"resourceId\": {\"videoId\": \""+videoId+"\",\"kind\": \"youtube#video\"},\"position\": 0}}";
 
        OutputStream os = conn.getOutputStream();
        os.write(input.getBytes());
        os.flush();
 
        if (conn.getResponseCode() != HttpURLConnection.HTTP_CREATED) {
            throw new RuntimeException("Failed : HTTP error code : "
                + conn.getResponseCode());
        }
 
        BufferedReader br = new BufferedReader(new InputStreamReader(
                (conn.getInputStream())));
 
        String output;
        System.out.println("Output from Server .... \n");
        while ((output = br.readLine()) != null) {
            System.out.println(output);
        }
 
        conn.disconnect();
 
      } catch (MalformedURLException e) {
 
        e.printStackTrace();
 
      } catch (IOException e) {
 
        e.printStackTrace();
 
     }
